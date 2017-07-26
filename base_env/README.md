# how to push docker image.

~~~~
docker login
docker build -t dtenpf/minipf_build --no-cache=true --build-arg http_proxy="xxxx" --build-arg https_proxy="xxxx" . 
docker tag <imageid> dtenpf/minipf_build:0.1
docker push denpf/minipf_build:0.1
~~~~

# how to create multi arch schroot
~~~~
# docker run --name "mybuild" --privileged -it dtenpf/minipf_build /bin/bash
# apt-get update
# apt-get install schroot debootstrap
# apt-get install qemu-user-static binfmt-support
# apt-get install git

** AMD64

# vi /etc/schroot/chroot.d/deploy_amd64.conf
[deploy_amd64]
type=directory
directory=/var/chroot/deploy_amd64
profile=default
users=root
root-groups=root

# mkdir -p /var/chroot/deploy_amd64
# debootstrap --variant=minbase sid /var/chroot/deploy_amd64 http://ftp.jp.debian.org/debian
# schroot -c deploy_amd64 /bin/bash

# vi /var/chroot/deploy_amd64/etc/apt/sources.list
deb http://ftp.jp.debian.org/debian sid main
deb [trusted=yes] file:///home/debian 

# mkdir -p /home/debian
# vi ./inst_pkg.sh
#!/bin/bash
apt-ftparchive packages . | gzip > Packages.gz

# chmod +x ./inst_pkg.sh

# cp *.deb /home/debian
# cd /home/debian
# ./inst_pkg.sh

** QEMU (There was the bug qemu_2.8.0, so I needed to compile.)

# apt-get install gcc-aarch64-linux-gnu
# apt-get build-dep qemu
# git clone git://git.qemu.org/qemu.git
# qemu/
# ./configure --target-list=aarch64-linux-user static
# make -j4
# cp aarch64-linux-user/qemu-aarch64 /usr/bin/qemu-aarch64-static

** AARCH64
# /etc/init.d/binfmt-support start
# update-binfmts --remove qemu-aarch64 /usr/bin/qemu-aarch64-static
# update-binfmts --import qemu-aarch64

# vi /etc/schroot/chroot.d/deploy_arm64.conf
[deploy_arm64]
type=directory
directory=/var/chroot/deploy_arm64
profile=default
users=root
root-groups=root

# mkdir -p /var/chroot/deploy_arm64
# qemu-debootstrap --variant=minbase --arch=arm64 sid /var/chroot/deploy_arm64/ http://ftp.jp.debian.org/debian

# vi /var/chroot/deploy_arm64/etc/apt/sources.list
deb http://ftp.debian.org/debian sid main

** ARM32
# mkdir -p /var/chroot/deploy_armhf
# qemu-debootstrap --variant=minbase --arch=armhf sid /var/chroot/deploy_armhf/ http://ftp.jp.debian.org/debian

# vi /var/chroot/deploy_armhf/etc/apt/sources.list
deb http://ftp.jp.debian.org/debian sid main
deb [trusted=yes] file:///home/debian 

# schroot -c deploy_amd64 /bin/bash
~~~~



