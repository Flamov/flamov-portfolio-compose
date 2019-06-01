FROM debian:jessie

RUN apt-get update && apt-get install -y cron bash wget
RUN mkdir -p /webroots/flamov.com/.well-known /scripts

WORKDIR /scripts
RUN wget https://dl.eff.org/certbot-auto
RUN chmod a+x ./certbot-auto

RUN /scripts/certbot-auto -n certificates

VOLUME /webroots
VOLUME /etc/letsencrypt

# Renew at 0300 every Monday
RUN echo "0 3 * * 1 root /scripts/certbot-auto renew" > /etc/cron.d/certbot

CMD ["cron", "-f"]
