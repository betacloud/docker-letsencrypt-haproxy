FROM dockercloud/haproxy:1.6.7
MAINTAINER Betacloud Solutions GmbH (https://www.betacloud-solutions.de)

RUN apk add --update --no-cache bash inotify-tools openssl \
	&& rm -rf /var/cache/apk/*

ENV LIVE_CERT_FOLDER="/etc/letsencrypt/live"
ENV PATH="/opt/haproxy/bin:$PATH"

COPY . /opt/haproxy

CMD ["entrypoint.sh", "dockercloud-haproxy"]
