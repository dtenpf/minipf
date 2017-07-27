# how to push docker image.

~~~~
docker login
docker build -t dtenpf/minipf_build --no-cache=true --build-arg http_proxy="xxxx" --build-arg https_proxy="xxxx" . 
docker tag <imageid> dtenpf/minipf_build:<tag>
docker push denpf/minipf_build:<tag>
~~~~

# how to create multi arch debian

~~~~
# docker run --name "mybuild" --privileged -it dtenpf/minipf_build /bin/bash

** AMD64(X86_64)
# mkdir -p /var/chroot/deploy_amd64
# debootstrap --variant=minbase sid /var/chroot/deploy_amd64 http://ftp.jp.debian.org/debian

# cp /root/sources.list /var/chroot/deploy_amd64/etc/apt/sources.list
# schroot -c deploy_amd64 /bin/bash
(deploy_amd64) # apt-get update
 
** ARM64(AARCH64)
# /etc/init.d/binfmt-support start
# update-binfmts --remove qemu-aarch64 /usr/bin/qemu-aarch64-static
# update-binfmts --import qemu-aarch64

# mkdir -p /var/chroot/deploy_arm64
# qemu-debootstrap --variant=minbase --arch=arm64 sid /var/chroot/deploy_arm64/ http://ftp.jp.debian.org/debian

# cp /root/sources.list /var/chroot/deploy_amd64/etc/apt/sources.list
# schroot -c deploy_amd64 /bin/bash
(deploy_arm64) # apt-get update
~~~~

# How to build QEMU

- コンパイル済みのデータが下記に置いてあります。
  - https://github.com/dtenpf/minipf/raw/master/extra/qemu-aarch64-static
- 備忘として手順を置いておきます。

~~~~
** QEMU (There was the bug qemu_2.8.0, so I needed to compile.)

# apt-get install gcc-aarch64-linux-gnu
# apt-get build-dep qemu
# git clone git://git.qemu.org/qemu.git
# qemu/
# ./configure --target-list=aarch64-linux-user static
# make -j4
# cp aarch64-linux-user/qemu-aarch64 /usr/bin/qemu-aarch64-static
~~~~
