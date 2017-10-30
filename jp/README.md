## Backpack

[このページ](https://ghc.haskell.org/trac/ghc/wiki/Backpack)の翻訳

これは Backpack のために作成されたページで，Edward が積極的にメンテナンスをしている(2017年8月現在)．

Backpack は実用的な Mix-In モジュールシステムで Haskell を改造するためのシステムである．
これは GHC8.2 と `cabal-install 2.0` で実装されているが，Stack ではサポートしていない．

Backpack の使い方に関するドキュメントは，現時点ではあちこちに点在している．
そのため，ここにはその最新のリファレンスが集まっているため便利である(GHC8.2のリリース前の2017-04-02現在)．

- 対になるブログ記事: Try Backpack, [`ghc --backpack`](http://blog.ezyang.com/2016/10/try-backpack-ghc-backpack) と [`Cabal packages`](http://blog.ezyang.com/2017/01/try-backpack-cabal-packages) にはCabalの有無にかかわらず，Backpack の主な機能を使用するための最新のチュートリアルがある．
- [`GHC manual section on module signatures`](https://downloads.haskell.org/~ghc/master/users-guide/separate_compilation.html#module-signatures)は Backpack の Signature ファイル(`hsig`)がどのように動作するかについての詳細な情報を説明してる．より読みやすいモノは Haskell wiki の [`Module signature`](https://wiki.haskell.org/Module_signature) にある．
- Cabal のページにはまだ Cabal でどのように働くかのマニュアルは無い．開発中です．
- Edward Z. Yang' の[論文](https://github.com/ezyang/thesis/releases)には Backpack の仕様と実装に関する詳細な情報が書かれている．また，ICFP2016 に提出した古い[論文](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/07/backpack-2016.pdf)もある．歴史的には [POPL2014の論文](http://plv.mpi-sws.org/backpack)もあるが，この頃より Backpack は劇的に変化している．
- Hackage にはまだ Backpack を用いたパッケージのアップロードのサポートがされていない．[next.hackage](http://next.hackage.haskell.org:8080)は，Backpackを処理するための開発ブランチで実行している Hackage インスタンスである．今のところ，Backpack 対応のパッケージはここにアップロードする必要がある．

Backpack を用いたコードはいくつかある．
以下のモノは良い例なので見てみると良いでしょう．

- [`backpack-str`](https://github.com/haskell-backpack/backpack-str)は，文字列の Signature と実装を定義している．これはかなり包括的で，パッケージは next.hackage で利用可能．
- [`streamy`](https://github.com/danidiaz/streamy)は "ストリーミング" ライブラリの Signature と実装を定義している(e.g. `conduit`, `pipes`, `streaming`)．
- [`haskell-opentracing`](https://github.com/ocharles/haskell-opentracing) は OpenTracing や Jaeger のバックエンドのための Signature を定義している．
- [`slay`](https://github.com/int-index/slay) は `Double` と `Int` の座標型でパラメーター化されたレイアウトエンジンである
- [`reflex-backpack`](https://github.com/ezyang/reflex-backpack) は Backpack'ing Reflex のクレイジーな実験の一種である．Reflex は多くの先進的なGHC機能を使用しており，Backpack ですべて処理をするためににイロイロあったが，何とか出来上がった！

古くなったドキュメント

- [Backpack specification.](https://github.com/ezyang/ghc-proposals/blob/backpack/proposals/0000-backpack.rst) これは私の論文に含まれていたが，一旦 Backpack が安定すれば，論文PDFをより Web フレンドリーな形式に戻す価値がある．
