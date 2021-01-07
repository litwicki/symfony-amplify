FROM nginx:alpine

RUN adduser -S -G www-data www-data
RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

EXPOSE 80 443

CMD ["nginx"]