FROM alpine:3.16.3

ARG REV=master
ARG APK_MIRROR=dl-cdn.alpinelinux.org

RUN sed -i "s/dl-cdn.alpinelinux.org/${APK_MIRROR}/g" /etc/apk/repositories
RUN apk update && apk upgrade
RUN rm /var/cache/apk/*
# Reference: https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem#alpine
RUN apk add argp-standalone asciidoc bash bc binutils bzip2 cdrkit coreutils \
  diffutils elfutils-dev findutils flex fts-dev g++ gawk gcc gettext git \
  grep intltool libxslt linux-headers make musl-libintl musl-obstack-dev \
  ncurses-dev openssl-dev patch perl python3-dev rsync tar unzip \
  util-linux wget zlib-dev --no-cache
# missing dependency workaround (libtinfo is not installable by any APK package,
# but can be simulated via libncurses (see: https://stackoverflow.com/a/41517423 )
# w/o this - ERROR: package/boot/uboot-mvebu failed to build (build variant: clearfog)
RUN ln -s /usr/lib/libncurses.so /usr/lib/libtinfo.so
# Utils needed
RUN apk add vim doas tmux --no-cache

# configure doas permission
RUN rm -r /etc/doas.d/*
RUN echo "permit nopass :wheel" >> /etc/doas.d/doas.conf

# use sudo if prefered
RUN apk add doas-sudo-shim --no-cache

# Setup user and work dir
RUN adduser -D wrt -G wheel
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
