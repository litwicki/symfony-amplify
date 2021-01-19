FROM nginx:alpine

RUN adduser -S -G www-data www-data

ADD nginx.conf /etc/nginx/
ADD symfony.conf /etc/nginx/conf.d/default.conf
RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

# Add self-signed certs for local only
RUN apk update \
    && apk add openssl \
    && openssl req \
    -subj '/CN=localhost/O=Amplify/C=US' \
    -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout \
    /etc/nginx/symfony.key -out /etc/nginx/symfony.crt

EXPOSE 80
EXPOSE 443

CMD ["nginx"]