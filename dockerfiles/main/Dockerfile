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
RUN apt install iputils-ping -y

# libgl dependencies
RUN apt-get install libgl1-mesa-glx -y
RUN apt-get install libglib2.0-0 -y

# Install django and dependencies
RUN pip install django
RUN pip install djangorestframework
RUN pip install django-cors-headers
RUN pip install psycopg2-binary
RUN pip install django-tinymce
RUN pip install pymysql
RUN pip install pillow
RUN pip install tzdata
RUN pip install qrcode
RUN pip install opencv-python==4.6.0.66
RUN pip install netifaces
RUN pip install pyftpdlib

# Main server
ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache
RUN git clone -b "Main" https://github.com/DCUSnSLab/LivingLab-CCS.git

WORKDIR /root/LivingLab-CCS/Livinglab_CMS/Livinglab/Livinglab-CMS/cms_main_server

# Service ports
EXPOSE 8000
EXPOSE 9021
EXPOSE 9999

CMD sh start_cms.sh
# CMD while true; do echo test; sleep 100; done