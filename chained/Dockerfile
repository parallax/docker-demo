FROM composer:1.6.2 as composer
# We're going to use a pre-built image for composer. Other people have already done the hard work installing it, there's no reason for us to reinvent the wheel.

# Next, we'll selectively add items to our composer image. The only things that composer needs to run are the composer.json and composer.lock files:
ADD composer.json /src/public/
ADD composer.lock /src/public/

# Now we'll run composer install:
RUN cd /src/public && \
  composer install


# Second FROM directive. This means we're starting from a clean slate - the above composer command's output exists *only* in the 'composer' container!
FROM prlx/nginx-php-fpm:7.1-clean

# Let's add the output of our composer step to the right place in our final image 
COPY --from=composer /src/public/vendor /src/public/vendor

# Now we'll add all of our source code (this directory) to /src/public (our webroot as configured in prlx/nginx-php-fpm:7.1-clean)
ADD / /src/public