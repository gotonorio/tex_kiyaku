# ソフィア・ガーデンズ川崎　管理規約

ソフィア・ガーデンズ川崎の管理規約TeXファイルです。

- kiyaku.tex（令和6年標準管理規約版）

- LaTeXエンジンはLuaLaTeX
- 文書クラスはjlreq  
- Cloud LaTeXでもコンパイルできることを確認済み。

- Dockerイメージとして paperist/alpine-texlive-ja を利用する。（公開を感謝）
- Macのlimaで確認済み。（Windowsの場合はWSL2で同じだと思う）

## limaによるdocker環境の作成

以下はターミナル環境で行う。

```bash
（1）limaの起動

    $ limactl start template://docker

（2）mountsを設定している行を検索して下記の追加修正をする。
　　 ※ mountしたディレクトリの書き込みを許可しますが、セキュリティには注意

    mounts:
      - location: "~"
    +   writable: true
      - location: "/tmp/lima"
        writable: true

（2-2）必要であれば下記の修正も行う。

    cpu: 2（デフォルト）
    memory: 4GiB（デフォルト）
    disk: 100GiB（デフォルト）

（3）linuxにログインしてLaTex用のdockerコンテナを生成する。

    $ limactl shell docker

（4）texファイルのあるディレクトリで以下を実行する。

    $ docker run --rm -it -v $PWD:/workdir paperist/texlive-ja:latest

（5）texファイルをコンパイルしてpdfファイルを作成。
    （コンパイル作業はtocファイル作成のため複数回実行する）

    $ lualatex texファイル名.tex
```
