# alpine-teamspeak3

[![](https://images.microbadger.com/badges/version/combro2k/alpine-teamspeak3.svg)](https://microbadger.com/images/combro2k/alpine-teamspeak3 "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/combro2k/alpine-teamspeak3.svg)](https://microbadger.com/images/combro2k/alpine-teamspeak3 "Get your own image badge on microbadger.com")

TeamSpeak 3 server running on Alpine with SQLite3 database

To start this container use:

~~~
docker run -d \
	-v /your/own/presistence/path:/teamspeak3 \
	-p 9987:9987/udp \
	-p 30033:30033 \
	-p 10011:10011 \
	--rm \
	combro2k/alpine-teamspeak3:latest
~~~
