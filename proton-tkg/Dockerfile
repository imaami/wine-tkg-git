FROM debian:unstable

RUN set -ex; \
	sed -Ei 's/(debian unstable main)$/\1 non-free contrib/' /etc/apt/sources.list; \
	apt-get -y update; \
	apt-get -y upgrade; \
	apt-get -y dist-upgrade; \
	apt-get -y --no-install-recommends install locales; \
	rm -rf /var/lib/apt/lists/*; \
	localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.UTF-8

RUN set -ex; \
	apt-get -y update; \
	apt-get -y upgrade; \
	apt-get -y --no-install-recommends install git; \
	git config --global user.name i; \
	git config --global user.email i@i; \
	git config --global pull.ff only; \
	git config --global alias.aliases "config --get-regex 'alias*'"; \
	git config --global alias.br "branch -avv --color"; \
	git config --global alias.idiff "diff -w -b --ignore-blank-lines --ignore-cr-at-eol --ignore-space-at-eol --color"; \
	git config --global alias.ilog "log -w -b --ignore-blank-lines --ignore-cr-at-eol --ignore-space-at-eol --color"; \
	git config --global alias.ishow "show -w -b --ignore-blank-lines --ignore-cr-at-eol --ignore-space-at-eol --color"; \
	git config --global alias.iwdiff "diff -w -b --ignore-blank-lines --ignore-cr-at-eol --ignore-space-at-eol --color --word-diff=color"; \
	git config --global alias.iwlog "log -w -b --ignore-blank-lines --ignore-cr-at-eol --ignore-space-at-eol --color --word-diff=color"; \
	git config --global alias.iwshow "show -w -b --ignore-blank-lines --ignore-cr-at-eol --ignore-space-at-eol --color --word-diff=color"; \
	git config --global alias.wdiff "diff --word-diff=color"; \
	git config --global alias.wlog "log --word-diff=color"; \
	git config --global alias.wshow "show --word-diff=color"; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	apt-get -y update; \
	apt-get -y upgrade; \
	apt-get -y --no-install-recommends install libc6-dev linux-libc-dev libnss3-dev libreadline-dev ca-certificates patch wget \
	        gnupg less fakeroot build-essential nano autoconf bison debhelper desktop-file-utils docbook-to-man docbook-utils \
	        docbook-xsl flex fontforge gawk gettext libacl1-dev libasound2-dev libcapi20-dev libcups2-dev libdbus-1-dev \
	        libgif-dev libglu1-mesa-dev libgphoto2-dev libgsm1-dev libgtk-3-dev libkrb5-dev liblcms2-dev libldap2-dev \
	        libmpg123-dev libncurses5-dev libopenal-dev libosmesa6-dev libpcap-dev libpulse-dev libsane-dev libssl-dev \
	        libtiff5-dev libudev-dev libv4l-dev libva-dev libxslt1-dev libxt-dev ocl-icd-opencl-dev oss4-dev prelink sharutils \
	        unixodbc-dev valgrind schedtool libfreetype6-dev xserver-xorg-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
	        gcc-multilib g++-multilib curl fonttools libsdl2-dev python3-tk libvulkan1 libkdb5-9 libppl14 libcolord2 libvulkan-dev \
	        libgnutls28-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev libpng-dev libkadm5clnt-mit11 libkadm5srv-mit11 \
	        libavcodec-dev libavutil-dev libswresample-dev libavcodec58 libswresample3 libavutil56 libfaudio0 libfaudio-dev libvkd3d-dev \
	        libxinerama-dev libxcursor-dev libxrandr-dev libxcomposite-dev mingw-w64 meson glslang-tools libgcrypt20 libgcrypt20-dev; \
	update-alternatives --set x86_64-w64-mingw32-gcc /usr/bin/x86_64-w64-mingw32-gcc-posix; \
	update-alternatives --set x86_64-w64-mingw32-g++ /usr/bin/x86_64-w64-mingw32-g++-posix; \
	update-alternatives --set i686-w64-mingw32-gcc /usr/bin/i686-w64-mingw32-gcc-posix; \
	update-alternatives --set i686-w64-mingw32-g++ /usr/bin/i686-w64-mingw32-g++-posix; \
	sed -Ei 's/^#[[:blank:]]*(.+history-search-.+)$/\1/' /etc/inputrc; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	apt-get -y update; \
	apt-get -y upgrade; \
	dpkg --add-architecture i386; \
	wget -O- https://dl.winehq.org/wine-builds/winehq.key | apt-key add -; \
	echo 'deb http://dl.winehq.org/wine-builds/debian bullseye main' > /etc/apt/sources.list.d/winehq.list; \
	echo 'deb-src http://dl.winehq.org/wine-builds/debian bullseye main' >> /etc/apt/sources.list.d/winehq.list; \
	apt-get -y update; \
	apt-get -y build-dep --only-source wine-staging/bullseye wine/bullseye; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	apt-get -y update; \
	apt-get -y upgrade; \
	mkdir -p /build; \
	cd /build; \
	git clone -b docker-wip-5.20 --depth=1 --single-branch https://github.com/imaami/wine-tkg-git.git; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	apt-get -y update; \
	apt-get -y upgrade; \
	cd /build/wine-tkg-git/proton-tkg; \
	./proton-tkg.sh || true; \
	rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
