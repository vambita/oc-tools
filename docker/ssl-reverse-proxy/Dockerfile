FROM nginx:latest

COPY ./conf/nginx.conf /etc/nginx/nginx.conf
COPY ./conf/default.conf /etc/nginx/conf.d/default.conf
COPY ./conf/includes/ /etc/nginx/includes/
COPY ./cert/ /etc/ssl/certs/nginx/