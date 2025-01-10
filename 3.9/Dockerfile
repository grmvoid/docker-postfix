FROM alpine:3.21

ARG POSTFIX_VERSION="3.9.1-r0"

ENV POSTFIX_MAILNAME="localhost" \
  POSTFIX_MESSAGE_SIZE_LIMIT=15728640 \
  POSTMASTER_ADDRESS="postmaster@localhost"

LABEL org.opencontainers.image.base.name="docker.io/library/alpine:3.21" \
  org.opencontainers.image.description="Application packaged by grmvoid" \
  org.opencontainers.image.documentation="https://github.com/grmvoid/docker-postfix/tree/master/README.md" \
  org.opencontainers.image.licenses="MIT" \
  org.opencontainers.image.ref.name="${POSTFIX_VERSION}" \
  org.opencontainers.image.source="https://github.com/grmvoid/docker-postfix/tree/master/3.9" \
  org.opencontainers.image.title="postfix" \
  org.opencontainers.image.vendor="grmvoid" \
  org.opencontainers.image.version="${POSTFIX_VERSION}"

COPY etc/ etc/
COPY docker-entrypoint /usr/local/bin/

RUN set -eux; \
  \
  # install deps
    apk add --no-cache \
      postfix=${POSTFIX_VERSION} \
      postfix-pcre=${POSTFIX_VERSION} \
      opendkim=2.11.0-r3 \
      opendkim-utils=2.11.0-r3 \
      opendmarc=1.4.2-r1; \
  # cleanup
    rm -rf /var/cache/apk/* \
      /tmp/* \
      /var/tmp/*;

VOLUME [ "/etc/postfix", "/var/spool/mail", "/etc/opendkim/keys" ]
EXPOSE 25/tcp 587/tcp

ENTRYPOINT [ "docker-entrypoint" ]
CMD [ "postfix", "-v", "start-fg" ]