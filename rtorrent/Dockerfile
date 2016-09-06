FROM alpine:3.4
MAINTAINER UmVnaXN0ZXIgcmVnaXN0ZXJkZWRpY2F0ZWQrZG9ja2VyKGF0KWdtYWlsLmNvbQo=

ENV USERNAME        admin
ENV PASSWORD=${PASSWORD:-$(hostname)}
ENV UID             1000
ENV GID             1000

# Let's roll
RUN set -xe && \
    apk add --no-cache --virtual .run-deps \
                                    apache2-utils \
                                    ffmpeg \
                                    ca-certificates \
                                    nginx \
                                    php5-fpm \
                                    php5-json \
                                    xmlrpc-c \
                                    libtorrent \
                                    curl \
                                    gzip \
                                    zip \
                                    unrar \
                                    supervisor \
                                    geoip && \
    apk add --no-cache --virtual .build-deps \
                                    build-base \
                                    git \
                                    automake \
                                    autoconf \
                                    cppunit-dev \
                                    openssl-dev \
                                    ncurses-dev \
                                    curl-dev && \
    cd /tmp && \
    curl -sSL https://github.com/Rudde/mktorrent/archive/v1.0.tar.gz | tar xz &&
    cd /tmp/mktorrent-1.0 && \
    make && make install && \

    git clone https://github.com/Novik/ruTorrent.git /var/www/rutorrent && \
    git clone https://github.com/xombiemp/rutorrentMobile.git /var/www/rutorrent/plugins/mobile && \
    git clone https://github.com/Phlooo/ruTorrent-MaterialDesign.git /var/www/rutorrent/plugins/theme/themes/materialdesign && \

    apk del .build-deps && \
    rm -rf /var/cache/apk/* /tmp/* \

COPY conf /

VOLUME /download
VOLUME /var/www/rutorrent/share/users

EXPOSE 8080 55000

CMD ["/usr/bin/startup"]