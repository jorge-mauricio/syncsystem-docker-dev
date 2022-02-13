# Variables.
ARG GIT_USER_NAME=Jorge Mauricio
ARG GIT_USER_EMAIL=web@jorgemauricio.com
ARG GIT_REPOSITORY_APPLICATION=https://github.com/jorge-mauricio/catalogo-v2.leroymerlin.com.br
ARG APPLICATION_DIRECTORY=catalogo-v2.leroymerlin.com.br

# Image.
FROM ubuntu

# Variables.
# NOTE: These variables must be in this part also in order to persist values.
ARG GIT_USER_NAME
ARG GIT_USER_EMAIL
ARG GIT_REPOSITORY_APPLICATION
ARG APPLICATION_DIRECTORY

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
RUN git config --global user.name ${GIT_USER_NAME}
#RUN git config --global user.email "web@jorgemauricio.com"
RUN git config --global user.email ${GIT_USER_EMAIL}

# copy files, etc


# Make directory to download files.
RUN mkdir downloads
RUN cd downloads

# Clone github repository (public).
# NOTE: Can be done with pull, but has to init git.
#RUN git clone https://github.com/jorge-mauricio/catalogo-v2.leroymerlin.com.br
RUN git clone ${GIT_REPOSITORY_APPLICATION}

# Copy donloaded files (github files) to root.
# TODO: update with the right directory name.
#RUN mv -v catalogo-v2.leroymerlin.com.br/* /var/www/html/
RUN mv -v ${APPLICATION_DIRECTORY}/* /var/www/html/
#RUN rm -r catalogo-v2.leroymerlin.com.br
RUN rm -r ${APPLICATION_DIRECTORY}
# DEBUG: cheche why when trying to dele the folder after copy, it´s not empty.

# Run apache automatically.
ENTRYPOINT apachectl -D FOREGROUND


# Especify environment variables.
# ENV name_of_variaval value_of_value