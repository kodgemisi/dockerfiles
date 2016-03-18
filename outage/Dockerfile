FROM ubuntu:14.04

RUN echo $PATH

#install git

RUN apt-get install git -y

#install wget

RUN apt-get install wget -y

#install python

RUN apt-get install python -y

#install casperjs

RUN git clone git://github.com/n1k0/casperjs.git
RUN cd casperjs
RUN ln -sf /casperjs/bin/casperjs /usr/local/bin/casperjs

#install phantomjs

RUN apt-get install libfontconfig -y
RUN mkdir -p /usr/local/src/phantomjs
WORKDIR /usr/local/src/phantomjs
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN tar xvf phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN ln -sf /usr/local/src/phantomjs/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/phantomjs
RUN ln -sf /usr/local/src/phantomjs/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/share/phantomjs
RUN ln -sf /usr/local/src/phantomjs/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/bin/phantomjs

RUN which phantomjs

#download water outage notifier from github
RUN cd /
WORKDIR /
RUN git clone https://github.com/kodgemisi/waterOutageNotifier

#run the script

WORKDIR waterOutageNotifier

ENTRYPOINT ["/waterOutageNotifier/run.sh"]
