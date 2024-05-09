FROM debian:bookworm

ARG REV=master
#ARG APT_MIRROR=deb.debian.org

#RUN sed -i "s/deb.debian.org/${APK_MIRROR}/g" /etc/apk/repositories
RUN apt update && apt upgrade -y

# Reference: https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem#debianubuntu
RUN apt install -y build-essential clang flex g++ gawk gcc-multilib gettext \
git libncurses5-dev libssl-dev python3-distutils rsync unzip zlib1g-dev

# Utils needed
RUN apt install -y wget file vim sudo tmux

# Clean apt cache
RUN apt clean

# configure sudo permission
RUN echo "wrt    ALL=(ALL:ALL) NOPASSWD: ALL" >> /etc/sudoers

# Setup user and work dir
RUN useradd -ms /bin/bash wrt
USER wrt

# Clone sources from upstream
WORKDIR /home/wrt
RUN git clone https://git.openwrt.org/openwrt/openwrt.git

# Enter workdir /home/wrt/openwrt
WORKDIR openwrt

# Change branch as needed
RUN git checkout ${REV}

# Start container with doing nothing by default
CMD ["sleep","infinity"]