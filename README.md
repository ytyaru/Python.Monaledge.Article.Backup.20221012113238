[ja](./README.ja.md)

# Monaledge.Article.Backup

Save all your articles written in Monalage in SQLite3. Only articles whose titles have been changed are subject to text update.

# DEMO

* [demo](https://ytyaru.github.io/Python.Monaledge.Article.Backup.20221012113238/)

![img](https://github.com/ytyaru/Python.Monaledge.Article.Backup.20221012113238/blob/master/doc/0.png?raw=true)

# Features

* sales point

# Requirement

* <time datetime="2022-10-12T11:32:31+0900">2022-10-12</time>
* [Raspbierry Pi](https://ja.wikipedia.org/wiki/Raspberry_Pi) 4 Model B Rev 1.2
* [Raspberry Pi OS](https://ja.wikipedia.org/wiki/Raspbian) buster 10.0 2020-08-20 <small>[setup](http://ytyaru.hatenablog.com/entry/2020/10/06/111111)</small>
* bash 5.0.3(1)-release
* Python 2.7.16
* Python 3.10.5
* [pyxel][] 1.3.1

[pyxel]:https://github.com/kitao/pyxel

```sh
$ uname -a
Linux raspberrypi 5.10.103-v7l+ #1529 SMP Tue Mar 8 12:24:00 GMT 2022 armv7l GNU/Linux
```

# Installation

Install Python 3.7 or higher.

Next, install [pyxel][] as follows.

* [pyxel/README](https://github.com/kitao/pyxel/blob/master/README.md#how-to-install)

```sh
sudo apt install python3 python3-pip libsdl2-dev libsdl2-image-dev
git clone https://github.com/kitao/pyxel.git
cd pyxel
make -C pyxel/core clean all
pip3 install .
```

# Usage

```sh
git clone https://github.com/ytyaru/Python.Monaledge.Article.Backup.20221012113238
cd Python.Monaledge.Article.Backup.20221012113238/src
./run.py
```

# Note

* important point

# Author

ytyaru

* [![github](http://www.google.com/s2/favicons?domain=github.com)](https://github.com/ytyaru "github")
* [![hatena](http://www.google.com/s2/favicons?domain=www.hatena.ne.jp)](http://ytyaru.hatenablog.com/ytyaru "hatena")
* [![twitter](http://www.google.com/s2/favicons?domain=twitter.com)](https://twitter.com/ytyaru1 "twitter")
* [![mastodon](http://www.google.com/s2/favicons?domain=mstdn.jp)](https://mstdn.jp/web/accounts/233143 "mastdon")

# License

This software is CC0 licensed.

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.en)

