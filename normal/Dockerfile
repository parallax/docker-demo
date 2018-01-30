FROM prlx/nginx-php-fpm:7.1-clean
# The above is an image we have built containing Nginx, PHP-FPM 7.1. Webroot is /src/public.

#Install composer to /usr/local/bin
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
  php -r "unlink('composer-setup.php');"

ADD / /src/public

RUN cd /src/public && \
  composer install