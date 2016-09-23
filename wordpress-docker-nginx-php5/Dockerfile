FROM ubuntu:16.04

# prerequisities
RUN apt-get update
RUN apt-get -y install software-properties-common python-software-properties
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get -y --allow-unauthenticated install nginx python-setuptools curl git unzip openssh-server openssl rsync
RUN apt-get -y --allow-unauthenticated install php5.6 php5.6-fpm php5.6-mysql php5.6-curl php5.6-gd php5.6-mbstring php5.6-mcrypt php5.6-xml php5.6-xmlrpc supervisor


# install wordpress

WORKDIR /
RUN wget http://wordpress.org/latest.tar.gz
RUN tar xzvf latest.tar.gz

#config

WORKDIR /wordpress
RUN rsync -avP /wordpress/ /usr/share/nginx/html/
WORKDIR /usr/share/nginx/html/
RUN mkdir /usr/share/nginx/html/wp-content/uploads
RUN chown -R root:www-data /usr/share/nginx/html/wp-content/uploads
RUN rm index.html
RUN mkdir /run/php/
RUN chown -R root:www-data /run/php

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD wp-config.php /usr/share/nginx/html/wp-config.php
RUN rm /etc/nginx/sites-enabled/default
ADD wordpress.conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/wordpress.conf /etc/nginx/sites-enabled/
RUN sed -i "s/AllowOverride None/AllowOverride All/g" /etc/nginx/nginx.conf

ENV MYSQL_DATABASE: wordpress
ENV MYSQL_USER: admin
ENV MYSQL_PASSWORD: 123456
ENV MYSQL_ROOT_PASSWORD: example

EXPOSE 80
VOLUME ["/usr/share/nginx/html/wp-content"]
CMD ["/usr/bin/supervisord", "-c" , "/etc/supervisor/conf.d/supervisord.conf"]
RUN chown -R root:www-data *
RUN chmod -R 775 *
