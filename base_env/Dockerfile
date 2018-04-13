FROM ubuntu:14.04
WORKDIR /root/
RUN apt-get update
RUN apt-get install -y vim cmake subversion smbclient wget libncurses5-dev libncursesw5-dev libc6-dev-i386 fakeroot p7zip-full gettext libexpat1-dev libxml2-utils libxml-xpath-perl bsdmainutils tar bsdmainutils zip unzip g++ pkg-config libasound2-dev zlib1g-dev
RUN apt-get install -y schroot debootstrap qemu-user-static binfmt-support git language-pack-ja
RUN wget https://cmake.org/files/v3.8/cmake-3.8.0-rc2-Linux-x86_64.sh
RUN chmod +x ./cmake-3.8.0-rc2-Linux-x86_64.sh
RUN ./cmake-3.8.0-rc2-Linux-x86_64.sh --skip-license --prefix=/usr/local/
RUN rm -f ./cmake-3.8.0-rc2-Linux-x86_64.sh
RUN wget https://github.com/dtenpf/minipf/raw/master/extra/qemu-aarch64-static
RUN chmod +x qemu-aarch64-static
RUN mv qemu-aarch64-static /usr/bin/
ADD deploy_arm64.conf /etc/schroot/chroot.d/
ADD deploy_amd64.conf /etc/schroot/chroot.d/
RUN mkdir -p /home/debian
ADD inst_pkg.sh /home/debian
RUN chmod +x /home/debian/inst_pkg.sh
ADD sources.list /home/debian/ 
RUN mkdir -p /var/chroot
RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y xz-utils
# Dotnetインストール
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y curl apt-transport-https genisoimage
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-trusty-prod trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
RUN cat /etc/apt/sources.list.d/dotnetdev.list
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y dotnet-runtime-2.0.5
# 環境変数設定
ENV USER user
ENV LANG ja_JP.UTF-8
