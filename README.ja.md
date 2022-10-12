[en](./README.md)

# Monaledge.Article.Backup

　モナレッジで書いた自分の記事をすべてSQLite3に保存する。タイトル変更された記事のみ本文更新対象とする。

<!--

# デモ

* [demo](https://ytyaru.github.io/Python.Monaledge.Article.Backup.20221012113238/)

![img](https://github.com/ytyaru/Python.Monaledge.Article.Backup.20221012113238/blob/master/doc/0.png?raw=true)

# 特徴

* セールスポイント

-->

# 開発環境

* <time datetime="2022-10-12T11:32:31+0900">2022-10-12</time>
* [Raspbierry Pi](https://ja.wikipedia.org/wiki/Raspberry_Pi) 4 Model B Rev 1.2
* [Raspberry Pi OS](https://ja.wikipedia.org/wiki/Raspbian) buster 10.0 2020-08-20 <small>[setup](http://ytyaru.hatenablog.com/entry/2020/10/06/111111)</small>
* bash 5.0.3(1)-release
* Python 3.10.5

```sh
$ uname -a
Linux raspberrypi 5.10.103-v7l+ #1529 SMP Tue Mar 8 12:24:00 GMT 2022 armv7l GNU/Linux
```

# インストール

```sh
git clone https://github.com/ytyaru/Python.Monaledge.Article.Backup.20221012113238
```

# 使い方

```sh
cd Python.Monaledge.Article.Backup.20221012113238/src
ADDRESS='モナレッジに登録した自分のモナコイン用アドレス'
./run.py $ADDRESS
./file.sh
```

ファイル|用途
--------|----
`run.py`|記事をバックアップする（WebAPIから記事を取得しSQLite3に保存する）
`file.sh`|記事をマークダウンファイルに出力する（SQLite3からマークダウンに出力する）

　`run.py`は第一引数にモナコイン用アドレスを渡すこと。

# 注意

* タイトルが更新されていない記事はDB更新されない

# 著者

　ytyaru

* [![github](http://www.google.com/s2/favicons?domain=github.com)](https://github.com/ytyaru "github")
* [![hatena](http://www.google.com/s2/favicons?domain=www.hatena.ne.jp)](http://ytyaru.hatenablog.com/ytyaru "hatena")
* [![twitter](http://www.google.com/s2/favicons?domain=twitter.com)](https://twitter.com/ytyaru1 "twitter")
* [![mastodon](http://www.google.com/s2/favicons?domain=mstdn.jp)](https://mstdn.jp/web/accounts/233143 "mastdon")

# ライセンス

　このソフトウェアはCC0ライセンスである。

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)

