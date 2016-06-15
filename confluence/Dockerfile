
# Basics

FROM ubuntu:14.04.3

ENV CONFLUENCE_VERSION 5.8.6
ENV CONFLUENCE_HOME /opt/confluence-home
ENV HOME /opt/confluence-home

# Install Java 8

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q software-properties-common

RUN echo "adding webupd8 repo"
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo "starts java8 installation"
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get -y install oracle-java8-installer && apt-get clean

# install confluence

RUN mkdir /opt/confluence && \
    mkdir /opt/confluence-home

RUN wget -O - \
    http://www.atlassian.com/software/confluence/downloads/binary/atlassian-confluence-${CONFLUENCE_VERSION}.tar.gz \
        | tar xzf - --strip=1 -C /opt/confluence \
    && perl -i -p -e 's/-Xms512m/-Xms128m/' /opt/confluence/bin/setenv.sh \
    && perl -i -p -e 's/-Xmx2048m/-Xmx512m/' /opt/confluence/bin/setenv.sh \
    && perl -i -p -e 's/_%T//' /opt/confluence/bin/setenv.sh \
    && echo "confluence.home = ${CONFLUENCE_HOME}" > \
        /opt/confluence/confluence/WEB-INF/classes/confluence-init.properties

WORKDIR /opt/confluence-home
VOLUME ["/opt/confluence-home"]

CMD ["/opt/confluence/bin/catalina.sh", "run"]
