# Pull base ubuntu image.
FROM ubuntu:14.04.3

# install python-software-properties (so you can do add-apt-repository)
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q software-properties-common

RUN echo "adding webupd8 repo"
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo "starts java8 installation"
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get -y install oracle-java8-installer && apt-get clean

RUN apt-get -y install curl

ENV BAMBOO_VERSION 5.9.7
ENV BAMBOO_HOME /opt/atlassian/application-data/bamboo-home

RUN mkdir /opt/bamboo
#download bamboo
RUN curl -Lks http://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-${BAMBOO_VERSION}.tar.gz -o /root/bamboo.tar.gz
RUN tar zxf /root/bamboo.tar.gz --strip=1 -C /opt/bamboo

RUN echo "bamboo.home = ${BAMBOO_HOME}" > /opt/bamboo/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties

VOLUME ["/opt/atlassian/application-data/bamboo-home"]
EXPOSE 8085

CMD ["/opt/bamboo/bin/catalina.sh", "run"]
