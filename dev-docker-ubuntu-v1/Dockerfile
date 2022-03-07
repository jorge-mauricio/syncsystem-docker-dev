# Variables.
ARG GIT_CONFIG_USER_NAME=Jorge Mauricio
ARG GIT_CONFIG_USER_EMAIL=web@jorgemauricio.com
ARG GIT_CONFIG_USER_ACCESS_KEY=${GIT_CONFIG_USER_ACCESS_KEY}
ARG GIT_CONFIG_APP_REPOSITORY=https://github.com/jorge-mauricio/catalogo-v2.leroymerlin.com.br
ARG CONFIG_APP_DIRECTORY=catalogo-v2.leroymerlin.com.br

# Image.
FROM ubuntu

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
#RUN git config --global user.name "Jorge Mauricio"
RUN git config --global user.name ${GIT_CONFIG_USER_NAME}
#RUN git config --global user.email "web@jorgemauricio.com"
RUN git config --global user.email ${GIT_CONFIG_USER_EMAIL}

# copy files, etc



# Make directory to download files.
RUN mkdir downloads
RUN cd downloads

# Make ssh directory.
#RUN mkdir /root/.ssh/

# Clone github repository (private - personal access key strategy).
RUN git clone https://oauth:${GIT_CONFIG_USER_ACCESS_KEY}@github.com/jorge-mauricio/react-ssr-boiler-plate-challenge-v1

# Clone github repository (public).
# NOTE: Can be done with pull, but has to init git.
#RUN git clone https://github.com/jorge-mauricio/catalogo-v2.leroymerlin.com.br
RUN git clone ${GIT_CONFIG_APP_REPOSITORY}

# Copy downloaded files (github files) to root.
# TODO: update with the right directory name.
#RUN mv -v catalogo-v2.leroymerlin.com.br/* /var/www/html/
RUN mv -v ${CONFIG_APP_DIRECTORY}/* /var/www/html/
#RUN rm -r catalogo-v2.leroymerlin.com.br
RUN rm -r ${CONFIG_APP_DIRECTORY}
# DEBUG: cheche why when trying to dele the folder after copy, it´s not empty.


# PHP 7.2 install.
#RUN apt-get -y install php7.2 php7.2-common php7.2-gd php7.2-mysql php7.2-imap php7.2-cli libapache2-mod-fcgid php-pear mcrypt imagemagick libruby libapache2-mod-python php7.2-curl php7.2-intl php7.2-pspell php7.2-recode php7.2-sqlite3 php7.2-tidy php7.2-xmlrpc php7.2-xsl memcached php-memcache php-imagick php-gettext php7.2-zip php7.2-mbstring php-soap
#RUN apt-get -y install php7.2-opcache php-apcu
#RUN apt-get -y install php7.2-fpm
#RUN apt -y install libmcrypt-dev php7.2-dev
#RUN pecl install mcrypt-1.0.1
  # NOTE: didn´t work yet.

# PHP 8 install.
#RUN apt install -y php8.0 libapache2-mod-php8.0
#RUN systemctl restart apache2
#RUN apt install php8.0-fpm libapache2-mod-fcgid
#RUN a2enmod proxy_fcgi setenvif
#RUN a2enconf php8.0-fpm
  # NOTE: didn´t work yet.

# PHP 8 install.
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php -y
RUN apt install php8.0 -y
RUN apt search php8.0-* -y
RUN apt install php8.0-gd php8.0-xml php8.0-soap php8.0-mbstring php8.0-mysql -y
RUN apt install libapache2-mod-php8.0 -y
#RUN a2enmod php8.0
#NOTE: For testing PHP install without docker file, and check if PHP is rendering, restart the container from outside the running container (it maintains everything installed in the container).
  # ex: terminal: docker restart <container>


# Dev helpers files - clone github repository (public).
RUN git clone https://github.com/jorge-mauricio/syncsystem-docker-dev
RUN mv  -v syncsystem-docker-dev/misc/phpcheck.php /var/www/html/
  # PHP check file.
RUN cp -a -b syncsystem-docker-dev/misc/php-config-files/linux/php8.0/php.ini /etc/php/8.0/apache2/php.ini
  # PHP 8.0 global config file.
RUN rm -r syncsystem-docker-dev



# Run apache automatically.
ENTRYPOINT apachectl -D FOREGROUND


# Especify environment variables.
# ENV name_of_variaval value_of_value