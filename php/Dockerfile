FROM php:5.6.11-fpm

ADD php.ini    /usr/local/etc/php/php.ini

ADD docker-php-pecl-install /usr/local/bin/
RUN chmod u+x /usr/local/bin/docker-php-pecl-install
#ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

#ADD redis.tar.gz /data/redis.tar.gz \
#	&& tar xfz /data/redis.tar.gz \
#	&& rm -r /data/redis.tar.gz \
#	&& mv phpredis-2.2.7 /usr/src/php/ext/redis \
#	&& docker-php-ext-install redis zip 

#RUN docker-php-ext-install gd \
RUN apt-get update
RUN apt-get install -y libssl-dev
RUN apt-get install -y cron

RUN docker-php-pecl-install mongo
RUN docker-php-pecl-install memcache

COPY redis.tgz /home/redis.tgz
#COPY memcached-2.0.1.tgz /home/memcached-2.0.1.tgz
RUN  docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install mysql \
	&& docker-php-ext-install mysqli \
    && pecl install /home/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini 
    #&& pecl install /home/memcached-2.0.1.tgz && echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini 


##    && docker-php-ext-install pdo_mysql \
##    && pecl install /home/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini
ADD composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer

RUN docker-php-pecl-install swoole
COPY memcache-3.0.8.tgz /home/memcache-3.0.8.tgz

RUN pecl install /home/memcache-3.0.8.tgz && echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini 
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install sockets


ADD phpv1.ini    /usr/local/etc/php/php.ini

WORKDIR /data
RUN usermod -u 1000 www-data

VOLUME ["/data"]