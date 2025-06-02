# ----------------------------------
# Environment: Postgres DB + cron
# ----------------------------------
FROM --platform=$TARGETOS/$TARGETARCH jojo1542/postgres_cron:15

LABEL maintainer="Parker <parker@pterodactyl.io>"

ENV DEBIAN_FRONTEND=noninteractive \
    HOME=/home/container

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
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
 && rm -rf /var/lib/apt/lists/*

RUN useradd -m -u 999 -d /home/container -s /usr/sbin/nologin container

USER container
WORKDIR /home/container
STOPSIGNAL SIGINT

COPY --chown=container:container ../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["tini", "-g", "--"]
CMD ["/entrypoint.sh"]
