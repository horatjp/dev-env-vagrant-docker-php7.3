FROM nginx:1.16

RUN apt-get update \
 && apt-get install -y openssl \
 && mkdir -p /var/www/public \
 && subject="/C=JP/ST=Tokyo/L=Chiyoda-ku" \
 && openssl req -new -newkey rsa:2048 -sha1 -x509 -nodes \
      -set_serial 1 \
      -days 365 \
      -subj "$subject" \
      -out "/etc/ssl/private/server.crt" \
      -keyout "/etc/ssl/private/server.key" \
 && chmod 400 /etc/ssl/private/server.*
