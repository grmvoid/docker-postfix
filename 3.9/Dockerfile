FROM alpine:3.21

ARG POSTFIX_VERSION="3.9.1-r0"

ENV POSTFIX_MAILNAME="localhost"
ENV POSTFIX_MESSAGE_SIZE_LIMIT=15728640
ENV POSTMASTER_ADDRESS="postmaster@localhost"

LABEL org.opencontainers.image.base.name="docker.io/library/alpine:3.21" \
      org.opencontainers.image.description="Application packaged by grmvoid" \
      org.opencontainers.image.documentation="https://github.com/grmvoid/docker-postfix/tree/master/README.md" \
      org.opencontainers.image.licenses="MIT" \
      org.opencontainers.image.ref.name="${POSTFIX_VERSION}" \
      org.opencontainers.image.source="https://github.com/grmvoid/docker-postfix/tree/master/3.9" \
      org.opencontainers.image.title="postfix" \
      org.opencontainers.image.vendor="grmvoid" \
      org.opencontainers.image.version="${POSTFIX_VERSION}"

COPY etc/* /etc/

RUN set -eux; \
    \
    # upgrade alpine \
      apk update; \
      apk upgrade; \
      apk add --no-cache \
        ca-certificates; \
      update-ca-certificates; \
    \
    # install deps
      apk add --no-cache \
        mailx \
        postfix=${POSTFIX_VERSION} \
        postfix-pcre=${POSTFIX_VERSION}; \
    # configure postfix \
      postconf -e myorigin="${POSTFIX_MAILNAME}"; \
      postconf -e myhostname="${POSTFIX_MAILNAME}"; \
      postconf -e mydestination="${POSTFIX_MAILNAME}"; \
      postconf -e message_size_limit="${POSTFIX_MESSAGE_SIZE_LIMIT}"; \
      postconf -e inet_protocols=ipv4; \
      postconf -e maillog_file=/dev/stdout; \
      echo "root: ${POSTMASTER_ADDRESS}" > /etc/aliases; \
      postalias /etc/aliases; \
      newaliases

VOLUME [ "/etc/postfix", "/var/mail", "/var/spool/mail" ]

EXPOSE 25/tcp 587/tcp
CMD [ "/usr/sbin/postfix", "start-fg" ]