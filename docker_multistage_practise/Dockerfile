ARG NGINX_VERSION=1.27.2-alpine
ARG STAGE

FROM nginx:${NGINX_VERSION} AS dev

WORKDIR /usr/share/nginx/html/dev

COPY ./dev .


FROM nginx:${NGINX_VERSION} AS prod

WORKDIR /usr/share/nginx/html/prod

COPY ./prod .

EXPOSE 80

