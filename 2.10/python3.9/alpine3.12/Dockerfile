FROM python:3.9-alpine3.12

WORKDIR /ansible
RUN apk --update --no-cache add \
        gnupg \
        openssh-client \
        ca-certificates \
        openssl \
    \
    && apk --update --no-cache add --virtual .build-deps \
        openssl-dev \
        libffi-dev \
        python3-dev \
        build-base \
    \
    && python3.9 -m pip install "ansible>=2.10,<2.11" jmespath prettytable \
    \
    && apk del .build-deps \
    && rm -rf /tmp/* \
    && rm -rf /var/cache/apk/*

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN ln -s /docker-entrypoint.sh /usr/local/bin/docker-entrypoint

STOPSIGNAL SIGTERM
ENTRYPOINT ["docker-entrypoint"]
CMD ["ansible-playbook"]