# ----------------------------------
# Environment: Postgres DB + cron
# ----------------------------------
FROM --platform=$TARGETOS/$TARGETARCH ghcr.io/jojo1542/postgres_cron:15

LABEL maintainer="Parker <parker@pterodactyl.io>"

ENV DEBIAN_FRONTEND=noninteractive \
    HOME=/home/container

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      netcat-openbsd \
      tini \
      curl \
      iproute2 \
      ca-certificates \
      fontconfig \
      git \
      openssl \
      sqlite3 \
      tar \
      tzdata \
 && rm -rf /var/lib/apt/lists/* \
 && useradd -d /home/container -m container -s /bin/bash

USER  container
ENV USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh

ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]