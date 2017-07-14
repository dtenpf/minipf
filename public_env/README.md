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
~~~~

- docker内で必要な設定ファイルをhostから共有する必要があり。そのひな形です。
- 社内環境でproxyが必要な方は.bashrcを編集してください。
- .smb.confは自分のID/PASSを入れてください

# How to run docker
~~~~
docker pull dtenpf/minipf_build:0.1
docker run --name my_build  -v <path to share dir>:/root/share -i -t dtenpf/minipf_build:0.1
~~~~

- In Docker
~~~~
/* 必要に応じて作業 */
# cp share/.bashrc /root
# cp share/.smb.conf /root
# cp share/local.user.conf /root
# mkdir /root/tmp

/* 毎回の作業 */
# export USER=user
# mkdir build_wk
# cd build_wk
# ./setup.sh <..to be continued>
~~~~

# How to reconnect docker
~~~~
docker start my_build
docker exec -it my_build /bin/bash
~~~~
# How to remove docker 
~~~~
docker rm my_build
~~~~
