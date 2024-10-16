ARG STAGE

FROM nginx:latest AS dev

WORKDIR /usr/share/nginx/html

COPY ./dev/ .

FROM nginx:latest AS prod

WORKDIR /usr/share/nginx/html

COPY ./prod/ .

FROM ${STAGE}

EXPOSE 80

