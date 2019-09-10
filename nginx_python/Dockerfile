FROM ubuntu:18.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y dist-upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -yq install net-tools nginx python-pip python3-dev

RUN pip install --upgrade pip
RUN pip install uwsgi supervisor

RUN useradd -ms /bin/bash serveradm
RUN usermod --groups www-data --append serveradm

RUN mkdir -p /home/serveradm/app
RUN mkdir -p /etc/uwsgi

COPY app/wsgi.py /home/serveradm/app/
#COPY etc/uwsgi/wsgi.ini /etc/uwsgi/wsgi.ini
COPY etc/uwsgi/wsgi.ini /home/serveradm/app/wsgi.ini
COPY etc/supervisord.conf /etc/supervisord.conf

EXPOSE 8080

#COPY nginx/sites-available /etc/nginx/sites-available
ENTRYPOINT ["/usr/local/bin/supervisord"]

