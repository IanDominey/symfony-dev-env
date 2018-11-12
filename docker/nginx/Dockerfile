FROM nginx:1-alpine

VOLUME /app
WORKDIR /app

RUN rm -f /etc/nginx/conf.d/default.conf

COPY ./docker/nginx/kt-ab.conf /etc/nginx/conf.d/site.conf

