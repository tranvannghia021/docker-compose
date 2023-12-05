ARG VERSION
FROM php:${VERSION}-fpm

RUN apt-get update -y
RUN apt-get -y install gcc make autoconf libc-dev pkg-config libzip-dev

RUN apt-get install -y --no-install-recommends \
	git \
	libmemcached-dev \
	libz-dev \
	libpq-dev \
	libssl-dev libssl-doc libsasl2-dev \
	libmcrypt-dev \
	libxml2-dev \
	zlib1g-dev libicu-dev g++ \
	libldap2-dev libbz2-dev \
	curl libcurl4-openssl-dev \
	libgmp-dev firebird-dev libib-util \
	re2c libpng++-dev \
	libwebp-dev libjpeg-dev libjpeg62-turbo-dev libpng-dev libxpm-dev libvpx-dev libfreetype6-dev \
	libmagick++-dev \
	libmagickwand-dev \
	zlib1g-dev libgd-dev \
	libtidy-dev libxslt1-dev libmagic-dev libexif-dev file \
	sqlite3 libsqlite3-dev libxslt-dev \
	libmhash2 libmhash-dev libc-client-dev libkrb5-dev libssh2-1-dev \
	unzip libpcre3 libpcre3-dev \
	poppler-utils ghostscript libmagickwand-6.q16-dev libsnmp-dev libedit-dev libreadline6-dev libsodium-dev \
	freetds-bin freetds-dev freetds-common libct4 libsybdb5 tdsodbc libreadline-dev librecode-dev libpspell-dev libonig-dev



#RUN docker-php-ext-install pdo_dblib
#RUN docker-php-ext-install bcmath bz2 calendar ctype curl dba dom
#RUN docker-php-ext-install fileinfo exif ftp gettext gmp
#RUN docker-php-ext-install intl ldap mbstring mysqli
#RUN docker-php-ext-install opcache pcntl pspell
#RUN docker-php-ext-install pdo_mysql pdo_pgsql pdo_sqlite pgsql phar posix
#RUN docker-php-ext-install session shmop simplexml soap sockets sodium
#RUN docker-php-ext-install sysvmsg sysvsem sysvshm
#RUN docker-php-ext-install snmp
#RUN docker-php-ext-install xml xsl
#RUN docker-php-ext-install tidy tokenizer zend_test zip
#RUN docker-php-ext-install filter

# install pecl extension
#RUN pecl install ds && \
#	pecl install imagick && \
#	pecl install igbinary && \
#	pecl install memcached && \
#	pecl install mcrypt && \
#	docker-php-ext-enable ds imagick igbinary memcached

RUN pecl install mongodb && docker-php-ext-enable mongodb
RUN yes "" | pecl install msgpack && \
	docker-php-ext-enable msgpack

# install APCu
RUN pecl install apcu && \
	docker-php-ext-enable apcu --ini-name docker-php-ext-10-apcu.ini

RUN apt-get update -y && apt-get install -y apt-transport-https locales gnupg

# install GD
RUN docker-php-ext-configure gd \
	--with-jpeg \
	--with-xpm \
	--with-webp \
	--with-freetype \
	&& docker-php-ext-install -j$(nproc) gd

# set locale to utf-8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'
#composer install


RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv ./composer.phar /usr/local/bin/composer

#RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
#RUN apt-get install -y nodejs \

WORKDIR /app
CMD ["php-fpm"]
EXPOSE 9000