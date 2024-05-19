# This image for OpenWRT build
# ref. https://openwrt.org/docs/guide-user/virtualization/obtain.firmware.docker
FROM debian:stretch-slim

ARG TARGETPLATFORM
ARG DEBIAN_FRONTEND=noninteractive
ARG userid
ARG groupid
ARG username

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# replace
RUN sed -i s/deb.debian.org/archive.debian.org/g /etc/apt/sources.list && \
    sed -i s/security.debian.org/archive.debian.org/g /etc/apt/sources.list && \
    sed -i s/stretch-updates/stretch/g /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y locales && \
    localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8


ENV LANG en_US.UTF-8

RUN apt install --no-install-recommends --no-install-suggests --yes \
        build-essential ccache ecj fastjar file g++ gawk gcc-multilib g++-multilib \
        gettext git java-propose-classpath libelf-dev libncurses5-dev \
        libncursesw5-dev libssl-dev python python2.7-dev python3 unzip wget \
        python3-setuptools python3-dev rsync subversion bc flex bison vim \
        swig time xsltproc zlib1g-dev ca-certificates curl device-tree-compiler && \
    apt-get clean && \
    rm -rf /var/lib/apt/* /var/cache/apt/* /tmp/* /var/tmp/*

RUN groupadd -g $groupid $username \
 && useradd -m -u $userid -g $groupid $username \
 && echo $username >/root/username

COPY gitconfig /home/$username/.gitconfig

RUN chown $userid:$groupid /home/$username/.gitconfig

ENV HOME=/home/$username
ENV USER=$username

WORKDIR $HOME

ENV HOME=/home/$username
ENV USER=$username
ENV WORKFOLDER=/home/$username/openwrt
ENV GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

ENTRYPOINT chroot --userspec=$(cat /root/username):$(cat /root/username) / /bin/bash -c "cd $WORKFOLDER && exec /bin/bash -i"
