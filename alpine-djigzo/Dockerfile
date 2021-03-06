FROM combro2k/alpine-base-glibc:latest

LABEL \
        org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.vcs-ref=$VCS_REF \
        org.label-schema.vcs-url="https://github.com/combro2k/dockerfiles/"

ENV \
	DJIGZO_MYSQL_DATABASE=djigzo \
	DJIGZO_MYSQL_USER=djigzo \
	DJIGZO_MYSQL_PASSWORD=djigzo \
	MYSQL_PORT_3306_TCP_ADDR=172.17.0.1 \
	MYSQL_PORT_3306_TCP_PORT=3306 \
	MAIL_CALLBACK_IP=172.17.0.1 \
	MAIL_CALLBACK_PORT=10026

RUN set -xe && apk add --no-cache --virtual=run-deps curl tar apache-ant openjdk8 bash openssl apr && \
	apk add --no-cache openssl-dev alpine-sdk apr-dev && \
	mkdir -p /app/djigzo /app/djigzo-web /app/tomcat8 /tmp/tomcat-native && \
	cd /app/djigzo && find /app/djigzo/conf -type f -exec dos2unix {} \; && /usr/bin/ant && chmod +x /app/djigzo/start-djigzo.sh && \
	curl -L -s  http://ftp.tudelft.nl/apache/tomcat/tomcat-8/v8.0.46/bin/apache-tomcat-8.0.46.tar.gz | \
	tar zx -C /app/tomcat8 --strip-components=1 && tar zx -C /tmp/tomcat-native -f /app/tomcat8/bin/tomcat-native.tar.gz --strip-components=1 && \
	cd /tmp/tomcat-native/native && ./configure \
		--with-java-home=/usr/lib/jvm/default-jvm \
		--with-apr=/usr/bin/apr-1-config --prefix=/app/tomcat8 \
		--libdir=/usr/java/packages/lib/amd64 --with-ssl=yes && \
	make && make install && rm -fr /tmp/tomcat-native && \
	rm -fr /app/tomcat8/webapps/* && mkdir -p /app/djigzo /app/djigzo-web && \
	curl --location --silent https://www.ciphermail.com/downloads/djigzo-release-3.2.7-5/djigzo_3.2.7-5.tar.gz | tar zx -C /app/djigzo && \
 	curl --location --silent https://www.ciphermail.com/downloads/djigzo-release-3.2.7-5/djigzo-web_3.2.7-5.tar.gz | tar zx -C /app/djigzo-web && \
	apk del --quiet --no-cache --progress openssl-dev alpine-sdk apr-dev && apk del --quiet --no-cache --progress --purge && \
	rm -rf /var/cache/apk/* && apk --no-cache --progress --quiet fix openssl

COPY resources/ /

EXPOSE 8443 8080 10025

ENTRYPOINT ["/init"]
