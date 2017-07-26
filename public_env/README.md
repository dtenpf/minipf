# Get your build / network configration files
~~~~
$ git clone https://github.com/dtenpf/minipf.git
$ cp -ar minipf/public_env/* <path to share dir>
$ ls -al <path to share dir>
total 7
drwxr-xr-x 1 hoge 197121   0 7月  14 12:20 ./
drwxr-xr-x 1 hoge 197121   0 7月  14 12:17 ../
-rw-r--r-- 1 hoge 197121 422 7月  14 12:18 .bashrc
-rw-r--r-- 1 hoge 197121  67 7月  14 12:20 .smb.conf
-rw-r--r-- 1 hoge 197121 334 7月  14 12:18 local.user.conf
-rwxr-xr-x 1 hoge 197121 126 7月  14 12:18 setup_minipf.sh
~~~~

- docker内で必要な設定ファイルをhostから共有するためのひな形です。
- 社内環境でproxyが必要な方は.bashrcを編集してください。
- .smb.confは自分のID/PASSを入れてください

# How to run docker
~~~~
docker pull dtenpf/minipf_build
docker run --name mybuild --privileged --ulimit msgqueue=12582912:12582912 -v <path to share dir>:/root/share -i -t dtenpf/minipf_build
~~~~

## In Docker
~~~~
/* 1回目のみ */
# /root/share/setup_minipf.sh
# . ~/.bashrc
~~~~

## Multi Arch Enviroment
- 隔離された環境でarm64/amd64のdebian環境が使えます。
- /homeが共有されており、APTリポジトリとなっているため、
　debianパッケージを配布することができます。packageを置いて、inst_pkg.shを叩いてください。
~~~~
# schroot -c deploy_arm64
# schroot -c deploy_amd64
~~~~~

- うまく動作しないときはbinfmtが止まっている場合があります。再起動させてください。

~~~~
# /etc/init.d/binfmt-support start
~~~~~


# How to reconnect docker
~~~~
docker start my_build
docker exec -it my_build /bin/bash
~~~~
# How to remove docker 
~~~~
docker rm my_build
~~~~
