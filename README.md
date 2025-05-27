# ソフィア・ガーデンズ川崎　管理規約

- kiyaku_2022.tex（令和3年標準管理規約版）
- liyaku_2025.tex（令和6年標準管理規約版）

- LaTeXエンジンはLuaLaTeX
- 文書クラスはjlreq  
- Cloud LaTeXでもコンパイルできることを確認済み。

- Dockerイメージとして paperist/alpine-texlive-ja を利用する。（公開を感謝）
- Macのlimaで確認済み。Windowsの場合はWSL2で同じだと思う（未確認）

## limaによるdocker環境の作成

以下はターミナル環境で行う。

```bash
（1）limaの起動

$ limactl start template://docker

起動時にconfigfileの修正を行う。

- mountsを設定している行を検索して下記の追加をする。
mounts:
  - location: "~"
+   writable: true
  - location: "/tmp/lima"
    writable: true

（2）linuxにログインしてLaTex用のdockerコンテナを生成する。
$ limactl shell docker

（3）texファイルのあるディレクトリで以下を実行する。
$ docker run --rm -it -v $PWD:/workdir paperist/texlive-ja:latest

（3）texファイルをコンパイルしてpdfファイルを作成。
    （コンパイル作業はtocファイル作成のため複数回実行する）
$ lualatex texファイル名.tex
```
