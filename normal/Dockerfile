FROM prlx/nginx-php-fpm:7.1-clean
# The above is an image we have built containing Nginx, PHP-FPM 7.1. Webroot is /src/public. This is prebuilt with a CMD entry to start Supervisor, which then in turn starts and watches nginx and php-fpm.
# We could of course start from alpine:3.7 or similar and then configure and install everything ourselves, but as this is repetitive (we'll be doing this for every build) and boring we're going to avoid doing so.

# Our site uses composer so we're going to need to install composer first:

#Install composer to /usr/local/bin
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
  php -r "unlink('composer-setup.php');"

# We're using a Makefile so we need make installed:
RUN apk add --no-cache make

# Now we'll add all of our source code (this directory) to /src/public (our webroot as configured in prlx/nginx-php-fpm:7.1-clean)
ADD / /src/public

# Finally we'll run make in the source folder to ensure our dependencies get installed
RUN cd /src/public && \
  make