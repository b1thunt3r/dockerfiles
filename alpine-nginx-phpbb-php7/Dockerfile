FROM combro2k/alpine-nginx-php7:latest

LABEL \
        org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.vcs-ref=$VCS_REF \
        org.label-schema.vcs-url="https://github.com/combro2k/dockerfiles/"

RUN set -xe && apk --quiet --no-cache add --virtual=run-deps php7-iconv php7-zlib php7-openssl php7-ctype php7-xml php7-pdo_mysql \
		php7-pdo php7-pdo_sqlite php7-zip php7-tokenizer && \
	mkdir /phpbb && chown www-data:www-data /phpbb -R && \
	curl -L https://www.phpbb.com/files/release/phpBB-3.2.1.tar.bz2 | tar jx -C /data/web --strip-components=1 && \
	chown www-data:www-data /data/web -R && \
	apk del --no-cache --progress --purge && rm -rf /var/cache/apk/*

COPY resources/ /

VOLUME /phpbb
