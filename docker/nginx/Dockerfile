FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y nginx nano
COPY nginx.conf /etc/nginx/nginx.conf
ADD sites-enabled /etc/nginx/sites-enabled
RUN rm /etc/nginx/sites-enabled/default
WORKDIR /var/www/html/app
CMD ["nginx"]