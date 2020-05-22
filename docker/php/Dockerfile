FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y
RUN apt-get install -y \
  nano \
  curl \
  wget \
  php-curl \
  php-fpm \
  php-gd \
  php-xsl \
  php-mysqlnd \
  php-cli \
  php-intl \
  php-bz2 \
  php-zip \
  php-mbstring \
  git \
  zip \
  php-apcu \
  php-opcache \
  php-xdebug
RUN mkdir /run/php
ADD conf/www.conf /etc/php/7.2/fpm/pool.d/www.conf
ADD conf/php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN ln -snf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
RUN echo "xdebug.idekey = PHPSTORM" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.default_enable=1" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_autostart = 1" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_port = 9001" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_handler = dbgp" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_host = host.docker.internal" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini

WORKDIR /var/www/html/app
CMD ["php-fpm7.2"]