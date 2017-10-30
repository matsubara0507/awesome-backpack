## Chap.2: A tutorial of Backpack’17

本章では，正規表現マッチャー(実装は [10] のを用いる)をモジュール化することで，Backpack'17 の主な機能をハイライトして，以降で詳述するコア概念のアイデアを紹介する
Haskell'98 や ML系言語について精通していることを仮定するが，Cabal(Haskellのパッケージマネージャー)や Backpack'14 については知らなくて良い．

### 2.1 A simple matcher in ’98

正規表現マッチャーを提供するHaskellライブラリを実装するように言われた．
了承し，Fischer, Huch and Wilke [10] の実装をコピーし， Fig2.2 のようなコードを書いた． 
これは，Haskell の `String`型による一般的なマッチャーで，Haskell'98 で書かれている．
また，このための小さなテストプログラムも書いた(Fig2.2のコト)．

```Haskell
-- Fig 2.1 Source code for a regular expression matcher from [10]

module Regex (Reg(..), accept) where

-- | A type of regular expressions.
data Reg = Eps | Sym Char | Alt Reg Reg | Seq Reg Reg | Rep Reg

-- | Check if a regular expression ’Reg’ matches a ’String’
accept :: Reg -> String -> Bool
accept Eps u = null u
accept (Sym c) u = u == [c]
accept (Alt p q) u = accept p u || accept q u
accept (Seq p q) u = or [accept p u1 && accept q u2 | (u1, u2) <- splits u]
accept (Rep r) u = or [and [accept r ui | ui <- ps] | ps <- parts u]

-- | Compute all splits of the string.
splits :: String -> [(String, String)]
splits [] = [([], [])]
splits (c:cs) = ([], c:cs):[(c:s1,s2) | (s1,s2) <- splits cs]

-- | Compute all possible non-empty partitions of the string
parts :: String -> [[String]]
parts [] = [[]]
parts [c] = [[[c]]]
parts (c:cs) = concat [[(c:p):ps, [c]:p:ps] | p:ps <- parts cs]
```

```Haskell
-- Fig 2.2 Simple test program for the matcher

module Main where

import Regex

nocs = Rep (Alt (Sym ’a’) (Sym ’b’))
onec = Seq nocs (Sym ’c’)
evencs = Seq (Rep (Seq onec onec)) nocs
main = print (accept evencs "acc")
```
