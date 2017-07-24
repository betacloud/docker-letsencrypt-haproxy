FROM alpine:3.6
MAINTAINER Betacloud Solutions GmbH (https://www.betacloud-solutions.de)

ARG VERSION
ENV VERSION ${VERSION:-latest}

RUN apk add --update --no-cache bash certbot tini \
	&& rm -rf /var/cache/apk/*

# Sets the HAProxy parameters to ensure this container
# handles letsencrypt traffic
ENV VIRTUAL_HOST="*/.well-known/acme-challenge/*"
ENV VIRTUAL_HOST_WEIGHT="999"
ENV PATH="/opt/letsencrypt/bin:$PATH"

COPY files/entrypoint.sh /opt/letsencrypt/entrypoint.sh
COPY files/update-certs.sh /opt/letsencrypt/update-certs.sh

# make sure we update certificates daily
RUN ln -fs /opt/letsencrypt/bin/update-certs.sh /etc/periodic/daily/

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["entrypoint.sh", "crond", "-f"]

EXPOSE 80
VOLUME /etc/letsencrypt
