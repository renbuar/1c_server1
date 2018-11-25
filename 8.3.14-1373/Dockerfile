FROM ubuntu:14.04
MAINTAINER temrdm

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository multiverse

RUN apt-get update
RUN apt-get install -y unixodbc libgsf-1-114 imagemagick libglib2.0-dev libt1-5 t1utils ttf-mscorefonts-installer
RUN apt-get install -y libusb-1.0-0 libc6-i386 mc make


RUN gpg --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/* \
        && curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture)" \
        && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture).asc" \
        && gpg --verify /usr/local/bin/gosu.asc \
        && rm /usr/local/bin/gosu.asc \
        && chmod +x /usr/local/bin/gosu \
        && apt-get purge -y --auto-remove curl

RUN apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
        && localedef -i ru_RU -c -f UTF-8 -A /usr/share/locale/locale.alias ru_RU.UTF-8

ENV LANG ru_RU.utf8

ENV SERVER_1C_VERSION 8.3.14-1373
ENV SERVER_1C_ARCH amd64
ENV DIST_SERVER_1C ./dist/
COPY 1c-enterprise83-common_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb /tmp
COPY 1c-enterprise83-server_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb /tmp


RUN if [ ! -f /tmp/1c-enterprise83-common_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb ]; then \
    echo File 1c-enterprise83-common_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb does not exist.; \
    echo "env DIST_SERVER_1C setted incorrectly. See README.md file."; \
    exit 1; fi

RUN if [ ! -f /tmp/1c-enterprise83-server_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb ]; then \
    echo File 1c-enterprise83-server_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb does not exist.; \
    echo "env DIST_SERVER_1C setted incorrectly. See README.md file."; \
    exit 1; fi

RUN dpkg -i /tmp/1c-enterprise83-common_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb \
            /tmp/1c-enterprise83-server_${SERVER_1C_VERSION}_${SERVER_1C_ARCH}.deb

RUN rm /tmp/*

RUN mkdir -p /home/usr1cv8/.1cv8/1C/1cv8/conf/
COPY logcfg.xml /home/usr1cv8/.1cv8/1C/1cv8/conf/
RUN chown -R usr1cv8:grp1cv8 /opt/1C
RUN mkdir -p /home/usr1cv8/dumps/
RUN mkdir -p /home/usr1cv8/log/
RUN chown -R usr1cv8:grp1cv8 /home/usr1cv8/
#VOLUME /home/usr1cv8/


COPY haspd-modules_7.60-eter1ubuntu_amd64.deb /tmp
COPY haspd_7.60-eter1ubuntu_amd64.deb /tmp

RUN if [ ! -f /tmp/haspd-modules_7.60-eter1ubuntu_amd64.deb ]; then \
    echo File haspd-modules_7.60-eter1ubuntu_amd64.deb does not exist.; \
    echo "env DIST_SERVER_1C setted incorrectly. See README.md file."; \
    exit 1; fi
RUN if [ ! -f /tmp/haspd_7.60-eter1ubuntu_amd64.deb ]; then \
    echo File haspd_7.60-eter1ubuntu_amd64.deb does not exist.; \
    echo "env DIST_SERVER_1C setted incorrectly. See README.md file."; \
    exit 1; fi


RUN dpkg -i /tmp/haspd-modules_7.60-eter1ubuntu_amd64.deb \
            /tmp/haspd_7.60-eter1ubuntu_amd64.deb

RUN rm /tmp/*

#COPY docker-entrypoint.sh /
#ENTRYPOINT ["/docker-entrypoint.sh"]

##ENTRYPOINT  /etc/init.d/haspd start && /opt/1C/v8.3/x86_64/ragent && /bin/bash
ENTRYPOINT  /etc/init.d/haspd start && gosu usr1cv8 /opt/1C/v8.3/x86_64/ragent
#ENTRYPOINT /etc/init.d/haspd start && gosu usr1cv8 /opt/1C/v8.3/x86_64/ragent /port 2540 /regport 2541 /range 2560:2591

EXPOSE 1540-1541 1560-1591 475 1947
#EXPOSE 2540-2541 2560-2591 475 1947
