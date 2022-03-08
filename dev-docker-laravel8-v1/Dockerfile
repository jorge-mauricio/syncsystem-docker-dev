# Variables.
ARG GIT_CONFIG_USER_NAME=Jorge Mauricio
ARG GIT_CONFIG_USER_EMAIL=web@jorgemauricio.com
ARG GIT_CONFIG_USER_ACCESS_KEY=${GIT_CONFIG_USER_ACCESS_KEY}
ARG GIT_CONFIG_APP_REPOSITORY=https://github.com/jorge-mauricio/laravel8
ARG CONFIG_APP_DIRECTORY=laravel8

# Image.
FROM ubuntu:20.04

# Variables.
# NOTE: These variables must be in this part also in order to persist values.
ARG GIT_CONFIG_USER_NAME
ARG GIT_CONFIG_USER_EMAIL
ARG GIT_CONFIG_USER_ACCESS_KEY
ARG GIT_CONFIG_APP_REPOSITORY
ARG CONFIG_APP_DIRECTORY

# Update repository.
RUN apt-get update

# Set timezone.
RUN apt install tzdata -y
ENV TZ="America/New_York"

# Install softwares.
RUN apt-get -y install apache2
# Git.
RUN apt-get -y install git
# Git - configure.
# TODO: update with right user and e-mail.
RUN git config --global user.name ${GIT_CONFIG_USER_NAME}
RUN git config --global user.email ${GIT_CONFIG_USER_EMAIL}

# CURL.
RUN apt-get install curl

# Nano.
RUN apt-get -y install nano

# Make directory to download files.
RUN mkdir downloads

# PHP repository.
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php -y

# PHP 8 install.
#RUN apt install software-properties-common -y
#RUN add-apt-repository ppa:ondrej/php -y
RUN apt install php8.0 -y
RUN apt search php8.0-* -y
RUN apt install php8.0-gd php8.0-xml php8.0-soap php8.0-mbstring php8.0-mysql -y
RUN apt install libapache2-mod-php8.0 -y

# PHP 7.3 install.
RUN apt install php7.3 -y
RUN apt search php7.3-* -y
RUN apt install php7.3-gd php7.3-xml php7.3-soap php7.3-mbstring php7.3-mysql -y
RUN apt install libapache2-mod-php7.3 -y


# Dev helpers files - clone github repository (public).
RUN git clone https://github.com/jorge-mauricio/syncsystem-docker-dev
RUN mv -v syncsystem-docker-dev/misc/phpcheck.php /var/www/html/
  # PHP check file.
RUN cp -a -b syncsystem-docker-dev/misc/php-config-files/linux/php8.0/php.ini /etc/php/8.0/apache2/
  # PHP 8.0 global config file.
RUN cp -a -b syncsystem-docker-dev/misc/php-config-files/linux/php7.3/php.ini /etc/php/7.3/apache2/
  # PHP 7.3 global config file.
#RUN rm -r syncsystem-docker-dev

# Install composer.
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Run apache automatically.
ENTRYPOINT apachectl -D FOREGROUND
