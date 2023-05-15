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
RUN apt install net-tools -y
RUN apt install jq -y

# Install django and dependencies
RUN pip install django
RUN pip install djangorestframework
RUN pip install django-cors-headers
RUN pip install psycopg2-binary
RUN pip install django-tinymce
RUN pip install pymysql
RUN pip install pillow
RUN pip install tzdata

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
# ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache
RUN git clone -b "Shelter" https://github.com/DCUSnSLab/LL_Shelter_API-Server.git

# CMS IDLE Page
# For refresh cache
ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache
RUN git clone -b "Sinage" https://github.com/DCUSnSLab/LL_Shelter_Sinage.git

# Add symbolic link to IDLE page
RUN ln -s /root/LL_Shelter_Sinage/Client/client_react/public simdir

WORKDIR /root/LL_Shelter_Sinage/Client/client_react
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm use --delete-prefix $NODE_VERSION && npm install"

WORKDIR /root/LL_Shelter_Sinage

# Service ports
EXPOSE 3000
EXPOSE 5000
EXPOSE 7000
EXPOSE 8000
EXPOSE 9021
EXPOSE 9999

CMD sh start_shelter.sh
# CMD while true; do echo test; sleep 100; done