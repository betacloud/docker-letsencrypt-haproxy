FROM dockercloud/haproxy:1.6.7
MAINTAINER Betacloud Solutions GmbH (https://www.betacloud-solutions.de)

ARG VERSION
ENV VERSION ${VERSION:-1.6.7}

RUN apk add --update --no-cache bash inotify-tools openssl \
	&& rm -rf /var/cache/apk/*

ENV LIVE_CERT_FOLDER="/etc/letsencrypt/live"
ENV PATH="/opt/haproxy/bin:$PATH"

COPY files/entrypoint.sh /opt/haproxy/bin/entrypoint.sh
COPY files/install-certs.sh /opt/haproxy/bin/install-certs.sh
COPY files/watch-certs.sh /opt/haproxy/bin/watch-certs.sh

CMD ["entrypoint.sh", "dockercloud-haproxy"]
