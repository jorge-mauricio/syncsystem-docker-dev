# Image.
FROM mysql:8.0.2

# Specify MySQL root password.
ENV MYSQL_ROOT_PASSWORD rootpwd

# Add database to be created.
ENV MYSQL_DATABASE dev_test1

# Add users to database
ENV MYSQL_USER ss_dev_db_user
ENV MYSQL_PASSWORD docK#1803


# Copy the scripts to docker-entrypoint-initdb.d/ which will automatically be executed during container startup.
  # MySQL scripts to create tables (.sql) and insert dummy items.
# COPY ./scripts/ /docker-entrypoint-initdb.d/

# Alternative for running a script.
# ref: https://youtu.be/w_aVnMmrASE?t=718
ADD setup.sql /docker-entrypoint-initdb.d


# Port mapping.
EXPOSE 3306

# Build instructions:
# terminal: sudo docker build -t . jorgemauriciodev/dev-docker-mysql-v1:latest
# Run instructions:
# terminal: sudo docker run --name dev-docker-container-mysql-v1 -d -p 3306:3306 jorgemauriciodev/dev-docker-mysql-v1:latest