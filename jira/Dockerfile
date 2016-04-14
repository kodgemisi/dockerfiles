
# Basics

FROM ubuntu:14.04.3

# Install Java 8

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q software-properties-common

RUN echo "adding webupd8 repo"
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo "starts java8 installation"
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get -y install oracle-java8-installer && apt-get clean

# Install JIRA

run apt-get install -q -y curl
run curl -Lks https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-7.1.4-jira-7.1.4.tar.gz -o /root/jira.tar.gz
run /usr/sbin/useradd --create-home --home-dir /usr/local/jira --shell /bin/bash jira
run mkdir -p /opt/jira
run tar zxf /root/jira.tar.gz --strip=1 -C /opt/jira
run mkdir -p /opt/jira-home
run echo "jira.home = /opt/jira-home" > /opt/jira/atlassian-jira/WEB-INF/classes/jira-application.properties

# Launching Jira

workdir /opt/jira-home
run rm -f /opt/jira-home/.jira-home.lock
expose 8080:8080
cmd ["/opt/jira/bin/start-jira.sh", "-fg"]
