FROM ubuntu:20.04

ENV TERM=xterm
ENV DEBIAN_FRONTEND=noninteractive
ENV PHP_INI=/etc/php/7.4/apache2/php.ini

COPY ./apache-entrypoint.sh /

RUN apt-get update \
    && apt-get install -y --no-install-recommends apache2 libapache2-mod-php libapache2-mod-security2 \
    curl ca-certificates openssl wget bzip2 php-gd php-json php-mysql php-curl php-mbstring \
    php-intl php-imagick php-xml php-zip php-bcmath php-gmp php-apcu php-redis \
    php-curl php-mime-type php-bz2 php-intl php-imagick php-cli \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/*


RUN	chmod o+x /apache-entrypoint.sh

COPY php.ini $PHP_INI
RUN chmod 644 $PHP_INI

VOLUME  /etc/apache2/
VOLUME  /etc/letsencrypt/
VOLUME	/var/www/

EXPOSE  80

ENTRYPOINT ["apachectl", "-D", "FOREGROUND"]
