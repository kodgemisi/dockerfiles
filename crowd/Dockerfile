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

ENV CROWD_VERSION 2.8.3
ENV CROWD_HOME /opt/atlassian/application-data/crowd-home

RUN mkdir /opt/crowd
#download crowd
RUN curl -Lks http://www.atlassian.com/software/crowd/downloads/binary/atlassian-crowd-${CROWD_VERSION}.tar.gz -o /root/crowd.tar.gz
RUN tar zxf /root/crowd.tar.gz --strip=1 -C /opt/crowd

RUN echo "crowd.home = ${CROWD_HOME}" > /opt/crowd/crowd-webapp/WEB-INF/classes/crowd-init.properties

VOLUME ["/opt/atlassian/application-data/crowd-home"]
EXPOSE 8095

CMD ["/opt/crowd/apache-tomcat/bin/catalina.sh", "run"]
