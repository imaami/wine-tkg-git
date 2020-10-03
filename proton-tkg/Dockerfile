FROM debian:unstable

RUN set -ex; \
	sed -Ei 's/(debian unstable main)$/\1 non-free contrib/' /etc/apt/sources.list; \
	apt-get update; \
	apt-get -y upgrade; \
	apt-get -y dist-upgrade; \
	apt-get -y --no-install-recommends install locales; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
	localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.UTF-8

RUN set -ex; \
	apt-get update; \
	apt-get -y --no-install-recommends install libc6-dev linux-libc-dev libreadline-dev ca-certificates patch git wget gnupg less \
	        fakeroot build-essential nano autoconf bison ccache debhelper desktop-file-utils docbook-to-man docbook-utils \
	        docbook-xsl flex fontforge gawk gettext libacl1-dev libasound2-dev libcapi20-dev libcups2-dev libdbus-1-dev \
	        libgif-dev libglu1-mesa-dev libgphoto2-dev libgsm1-dev libgtk-3-dev libkrb5-dev liblcms2-dev libldap2-dev \
	        libmpg123-dev libncurses5-dev libopenal-dev libosmesa6-dev libpcap-dev libpulse-dev libsane-dev libssl-dev \
	        libtiff5-dev libudev-dev libv4l-dev libva-dev libxslt1-dev libxt-dev ocl-icd-opencl-dev oss4-dev prelink sharutils \
	        unixodbc-dev valgrind schedtool libfreetype6-dev xserver-xorg-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
	        gcc-multilib g++-multilib curl fonttools libsdl2-dev python3-tk libvulkan1 libkdb5-9 libppl14 libcolord2 libvulkan-dev \
	        libgnutls28-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev libpng-dev libkadm5clnt-mit11 libkadm5srv-mit11 \
	        libavcodec-dev libavutil-dev libswresample-dev libavcodec58 libswresample3 libavutil56 libfaudio0 libfaudio-dev libvkd3d-dev \
	        libxinerama-dev libxcursor-dev libxrandr-dev libxcomposite-dev mingw-w64; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	dpkg --add-architecture i386; \
	wget -O- https://dl.winehq.org/wine-builds/winehq.key | apt-key add -; \
	echo 'deb http://dl.winehq.org/wine-builds/debian bullseye main' > /etc/apt/sources.list.d/winehq.list

RUN set -ex; \
	apt-get update; \
	apt-get -y --install-recommends install wine-devel-amd64 wine-staging-amd64; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	mkdir -p /build; \
	cd /build; \
	git clone -b docker-wip --depth=1 --single-branch https://github.com/imaami/wine-tkg-git.git

## What to install for the 32-bit build:
#RUN set -ex; \
#	apt-get update; \
#	apt-get -y --install-recommends install wine-devel wine-staging; \
#	apt-get -y --no-install-recommends install xserver-xorg-dev:i386 libfreetype6-dev:i386 libfontconfig1-dev:i386 libglu1-mesa-dev:i386 \
#	        libosmesa6-dev:i386 libvulkan-dev:i386 libvulkan1:i386 libpulse-dev:i386 libopenal-dev:i386 libncurses-dev:i386 libfaudio0:i386 \
#	        libfaudio-dev:i386 libvkd3d-dev:i386 libgnutls28-dev:i386 libtiff-dev:i386 libldap-dev:i386 libcapi20-dev:i386 libpcap-dev:i386 \
#	        libxml2-dev:i386 libmpg123-dev:i386 libgphoto2-dev:i386 libsane-dev:i386 libcupsimage2-dev:i386 libkrb5-dev:i386 libgsm1-dev:i386 \
#	        libxslt1-dev:i386 libv4l-dev:i386 libgstreamer-plugins-base1.0-dev:i386 libudev-dev:i386 libxi-dev:i386 liblcms2-dev:i386 \
#	        libibus-1.0-dev:i386 libsdl2-dev:i386 ocl-icd-opencl-dev:i386 libxinerama-dev:i386 libxcursor-dev:i386 libxrandr-dev:i386 \
#	        libxcomposite-dev:i386 libavcodec58:i386 libswresample3:i386 libavutil56:i386; \
#	apt-get clean; \
#	rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
