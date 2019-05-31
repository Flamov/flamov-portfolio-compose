FROM debian:jessie

RUN apt-get update && apt-get install -y cron bash wget
RUN mkdir -p /webroots/flamov.com/.well-known /scripts

WORKDIR /scripts
RUN wget https://dl.eff.org/certbot-auto
RUN chmod a+x ./certbot-auto

RUN /scripts/certbot-auto -n certificates

VOLUME /webroots
VOLUME /etc/letsencrypt

RUN echo "00 05 * * 2,4,6,7 root /scripts/certbot-auto renew" > /etc/cron.d/certbot

CMD ["cron", "-f"]
