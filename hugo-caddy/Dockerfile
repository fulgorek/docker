FROM alpine:latest

MAINTAINER Alejandro Torres <fulgorek@gmail.com>

ARG HUGO_VERSION
ENV HUGO_VERSION=${HUGO_VERSION:-0.16}

ARG CADDY_VERSION
ENV CADDY_VERSION=${CADDY_VERSION:-0.9.0}

ARG CADDY_AUTH_LOCATION
ENV CADDY_AUTH_LOCATION=${CADDY_AUTH_LOCATION:-/admin}

ARG CADDY_USER
ENV CADDY_USER=${CADDY_USER:-admin}

ARG CADDY_PASS
ENV CADDY_PASS=${CADDY_PASS:-admin}

RUN apk add --update wget ca-certificates && \
  cd /tmp/ && \
  wget "https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_linux-64bit.tgz" -O hugo_linux-64bit.tgz && \
  tar xzf hugo_linux-64bit.tgz && \
  mv hugo /usr/bin/hugo && \
  wget "https://caddyserver.com/download/build?os=linux&arch=amd64&features=git%2Chugo%2Cminify%2Crealip" -O caddy.tar.gz && \
  tar xzf caddy.tar.gz && \
  mv caddy /usr/bin/caddy && \
  apk del wget ca-certificates && \
  mkdir -p /var/caddy/ && \
  rm -rf /tmp/* /var/cache/apk/*

COPY ./Caddyfile /var/caddy/Caddyfile

VOLUME /site

VOLUME /var/caddy

WORKDIR /site

CMD ["/usr/bin/caddy", "-conf=/var/caddy/Caddyfile"]

EXPOSE 80
