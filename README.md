# tex_kiyaku

Docker コンテナによるLaTeX環境
- Dockerイメージとして paperist/alpine-texlive-ja を利用する。
- ダウンロード出来ない場合はDockerfileでbuildすればよい。（公開を感謝）
- 目次を生成する場合、uplatex kiyaku.texを複数回実行する必要がある。
  したがって、本来なら下記のコマンドでpdfファイルが作成されるが、目次が作成されない。
  $ docker run --rm -v $PWD:/workdir paperist/alpine-texlive-ja uplatex kiyaku.tex
  $ docker run --rm -v $PWD:/workdir paperist/alpine-texlive-ja dvipdfmx kiyaku.dvi

- 以下のコマンドでtex_containerという名前のDockerコンテナをダウンロードして起動、ログインする。
  $ docker run -it --name tex_container --rm -v $PWD:/workdir paperist/alpine-texlive-ja

    -it : コンテナにログインしてシェル操作可能にする。
    --name : コンテナに名前を設定する。
    --rm : コンテナを終了したらコンテナを破棄する。
    -v : ホストのパス(コマンドを起動したディレクトリ)をコンテナのパス(/workdir)にマウントする。
- コンテナにログインしている状態なので、texファイルがあるディレクトリに移動してコンパイルする。
  コンパイルは目次を生成するため複数回実行する。\\
  $ uplatex kiyaku.tex
- コンパイルされたdviファイルをpdfファイルに変換する。\\
  $ dvipdfmx kiyaku.dvi
- これでkiyaku.pdfが作成される。

Dockerfileから環境設定
- imageを作成。
  Dockerfileと同じディレクトリで以下のコマンドを実行。（ドットを忘れないこと）
  $ docker build -t イメージ名 .
- imageからコンテナを起動。
  texファイルが存在するディレクトリをマウントするので、どこでコマンドを実行するか
  気をつけること。
  $ docker run -it --name tex_container --rm -v $PWD:/workdir イメージ名
  
