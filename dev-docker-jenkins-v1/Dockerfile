# Image.
FROM ubuntu

# Update repository.
RUN apt-get update

# Set timezone.
RUN apt install tzdata -y
ENV TZ="America/New_York"

# Install softwares.

# wget.
RUN apt-get install wget - y
# gnupg.
RUN apt-get install -y gnupg

# Install jenkins.
RUN apt-get install default-jdk - y

# Install apache2.
RUN apt-get install apache2 - y

# Donwload package.
#RUN wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  #Outdated info.
RUN wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | apt-key add -

#RUN sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
  #Outdated info.
#RUN sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \ /etc/apt/sources.list.d/jenkins.list'
RUN sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

RUN apt-get update

RUN apt-get install jenkins -y