FROM combro2k/alpine-nginx-php5:latest

LABEL \
        org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.vcs-ref=$VCS_REF \
        org.label-schema.vcs-url="https://github.com/combro2k/dockerfiles/"

RUN set -xe && apk --quiet --no-cache add --virtual=run-deps php5-iconv php5-zlib php5-imap php5-openssl php5-ctype && \
	cd /data && curl --location --silent https://github.com/shaarli/Shaarli/archive/latest.tar.gz | tar zx -C /data/web --strip-components=1 && \
	chown www-data:www-data /data/web -R && cd /data/web && /usr/bin/composer install --no-dev && \
	apk del --quiet --no-cache --progress --purge && rm -rf /var/cache/apk/*

VOLUME /data/web/data
