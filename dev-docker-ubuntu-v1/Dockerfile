# Variables.
ARG GIT_CONFIG_USER_NAME=Jorge Mauricio
ARG GIT_CONFIG_USER_EMAIL=web@jorgemauricio.com
ARG GIT_CONFIG_APP_REPOSITORY=https://github.com/jorge-mauricio/catalogo-v2.leroymerlin.com.br
ARG CONFIG_APP_DIRECTORY=catalogo-v2.leroymerlin.com.br

# Image.
FROM ubuntu

# Variables.
# NOTE: These variables must be in this part also in order to persist values.
ARG GIT_CONFIG_USER_NAME
ARG GIT_CONFIG_USER_EMAIL
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

# Clone github repository (public).
# NOTE: Can be done with pull, but has to init git.
#RUN git clone https://github.com/jorge-mauricio/catalogo-v2.leroymerlin.com.br
RUN git clone ${GIT_CONFIG_APP_REPOSITORY}

# Copy donloaded files (github files) to root.
# TODO: update with the right directory name.
#RUN mv -v catalogo-v2.leroymerlin.com.br/* /var/www/html/
RUN mv -v ${CONFIG_APP_DIRECTORY}/* /var/www/html/
#RUN rm -r catalogo-v2.leroymerlin.com.br
RUN rm -r ${CONFIG_APP_DIRECTORY}
# DEBUG: cheche why when trying to dele the folder after copy, it´s not empty.


# Dev helpers files - clone github repository (public).
RUN git clone https://github.com/jorge-mauricio/syncsystem-docker-dev
RUN mv  -v syncsystem-docker-dev/misc/phpcheck.php /var/www/html/
  # PHP check file.
RUN rm -r syncsystem-docker-dev

# Run apache automatically.
ENTRYPOINT apachectl -D FOREGROUND


# Especify environment variables.
# ENV name_of_variaval value_of_value