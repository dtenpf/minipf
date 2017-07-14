FROM ubuntu:14.04
WORKDIR /root/
RUN apt-get update
RUN apt-get install -y vim cmake subversion smbclient wget libncurses5-dev libncursesw5-dev libc6-dev-i386 fakeroot p7zip-full gettext libexpat1-dev libxml2-utils libxml-xpath-perl bsdmainutils tar bsdmainutils zip unzip
RUN wget https://cmake.org/files/v3.8/cmake-3.8.0-rc2-Linux-x86_64.sh
RUN chmod +x ./cmake-3.8.0-rc2-Linux-x86_64.sh
RUN ./cmake-3.8.0-rc2-Linux-x86_64.sh --skip-license --prefix=/usr/local/
RUN rm -f ./cmake-3.8.0-rc2-Linux-x86_64.sh
