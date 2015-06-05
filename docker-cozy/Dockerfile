FROM debian:latest
MAINTAINER Christophecharrier christophecharrier@sfr.fr

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update
RUN apt-get install -y apt-utils python python-pip python-dev software-properties-common wget sudo openssh-server
RUN pip install fabric fabtools
RUN wget --no-check-certificate https://raw.githubusercontent.com/cozy/cozy-setup/master/fabfile.py
RUN useradd sudoer
RUN echo "sudoer ALL=(ALL:ALL) ALL" >> /etc/sudoers
RUN echo "sudoer:hi" | chpasswd
RUN mkdir /home/sudoer
RUN chown sudoer /home/sudoer
RUN echo "env={'password': 'hi'}" > ./fabfile2.py
RUN cat ./fabfile.py >> ./fabfile2.py
RUN /etc/init.d/ssh start && fab -H sudoer@localhost install -f ./fabfile2.py --password=hi
RUN userdel sudoer

EXPOSE 80 443 9104 
CMD supervisord -n -c /etc/supervisor/supervisord.conf
