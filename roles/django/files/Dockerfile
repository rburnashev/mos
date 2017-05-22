############################################################
# Dockerfile to run a Django-based web application
############################################################

# Set the base image to use to Debian
FROM debian:latest

# Set the file maintainer (your name - the file's author)
MAINTAINER Roman Burnashev

# Set env variables used in this Dockerfile (add a unique prefix, such as DOCKYARD)
# Directory in container for all project files
ENV WORK_DIR=/srv
# Directory in container for project source files
ENV PROJECT=projectname

# Install required packages and remove the apt packages cache when done.

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
    git \
    python \
    python-dev \
    python-setuptools \
    python-pip \
    libpq-dev && \
    pip install -U pip setuptools && \
   rm -rf /var/lib/apt/lists/*

# install uwsgi
RUN pip install uwsgi

# Clone app repository
WORKDIR $WORK_DIR
RUN git clone git://github.com/kirpit/django-sample-app.git $PROJECT

workdir $PROJECT

# rename project folder 
#RUN mv projectname $PROJECT

# Install Python dependencies
RUN pip install -r requirements.txt

# setting project name
RUN sed -i "s/{{ project_name }}/$PROJECT/g" ./$PROJECT/settings/default.py
RUN sed -i "s/{{ project_name }}/$PROJECT/" ./$PROJECT/wsgi.py
#RUN sed -i "s/projectname/$PROJECT/" ./$PROJECT/urls.py

# Copy local config for db connect
ADD local.py $WORK_DIR/$PROJECT/$PROJECT/settings/local.py

#Start migration script
workdir $PROJECT
RUN ./manage.py migrate

#Start app
CMD ./manage.py runserver 0.0.0.0:8000

# Port to expose
EXPOSE 8000

