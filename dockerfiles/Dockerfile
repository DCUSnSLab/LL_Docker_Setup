# CMS Shelter server dockerfile

FROM ubuntu:22.04

MAINTAINER snslabdocker

WORKDIR /root

RUN apt-get update -y

RUN apt-get install vim -y

RUN apt-get install python3 -y
RUN apt-get install pip -y

RUN apt-get install git -y
RUN apt install curl -y

# Install django and dependencies
RUN pip install django
RUN pip install djangorestframework
RUN pip install django-cors-headers
RUN pip install psycopg2-binary
RUN pip install django-tinymce
RUN pip install pymysql
RUN pip install pillow

# Install Websocket based IDLE page server dependencies
RUN pip install schedule
RUN pip install websockets
RUN pip install tabulate

# Install nvm and npm env
RUN mkdir -p /usr/local/nvm
ENV NVM_DIR /usr/local/nvm
# IMPORTANT: set the exact version
ENV NODE_VERSION 16.17.0
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION && nvm use --delete-prefix $NODE_VERSION"
# add node and npm to the PATH
ENV NODE_PATH $NVM_DIR/versions/node/$NODE_VERSION/bin
ENV PATH $NODE_PATH:$PATH

# Shelter server (Django based db construct)
RUN git clone -b "Shelter" https://github.com/DCUSnSLab/LivingLab-ShelterServer.git

# CMS IDLE Page
RUN git clone -b "LP-58_idle" https://github.com/DCUSnSLab/LivingLab-CMS-IDLE.git

WORKDIR /root/LivingLab-CMS-IDLE/Client/client_react
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm use --delete-prefix $NODE_VERSION && npm install"

WORKDIR /root/LivingLab-CMS-IDLE
# Service ports
EXPOSE 3000
EXPOSE 5000
EXPOSE 8000
EXPOSE 9021
EXPOSE 9999

CMD sh start_shelter.sh
# CMD while true; do echo test; sleep 100; done