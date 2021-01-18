FROM nginx:alpine

WORKDIR /etc/nginx

RUN apk update \
    && apk add openssl

RUN rm conf.d/default.conf
ADD ./conf.d/* conf.d/
ADD entrypoint.sh ./entrypoint.sh

RUN sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/symfony.key -out /etc/nginx/symfony.crt

CMD ["nginx"]

EXPOSE 80 443