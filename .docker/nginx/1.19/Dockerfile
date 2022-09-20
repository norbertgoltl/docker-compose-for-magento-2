FROM nginx:1.19

ENV PHP_HOST=phpfpm
ENV PHP_PORT=9000
ENV APP_MAGE_MODE=default

COPY ./nginx.conf /etc/nginx/
COPY ./magento2-cors.conf /etc/nginx/
COPY ./default.conf /etc/nginx/conf.d/

WORKDIR /var/www/html
