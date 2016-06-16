FROM ubuntu:14.04.3

# prerequisities

RUN apt-get update
RUN apt-get -y install apache2 python-setuptools curl git unzip openssh-server openssl rsync 
RUN apt-get -y install mysql-client php5-mysql php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-memcached php5-ming php5-ps php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl libssh2-php libapache2-mod-php5

# install wordpress

WORKDIR /
RUN wget http://wordpress.org/latest.tar.gz
RUN tar xzvf latest.tar.gz

#config

WORKDIR /wordpress
RUN rsync -avP /wordpress/ /var/www/html/
WORKDIR /var/www/html/
RUN mkdir /var/www/html/wp-content/uploads
RUN chown -R :www-data /var/www/html/wp-content/uploads
RUN rm index.html

ADD .htaccess /var/www/html/.htaccess
ADD wp-config.php /var/www/html/wp-config.php
ADD wordpress.conf /etc/apache2/sites-available/
RUN ln -s /etc/apache2/sites-available/wordpress.conf /etc/apache2/sites-enabled/
RUN sed -i "s/AllowOverride None/AllowOverride All/g" /etc/apache2/apache2.conf
RUN a2enmod php5
RUN a2enmod rewrite

ENV MYSQL_DATABASE: database name
ENV MYSQL_USER: user name
ENV MYSQL_PASSWORD: password
ENV MYSQL_ROOT_PASSWORD: example

EXPOSE 80
VOLUME ["/var/www/html/wp-content"]
CMD /usr/sbin/apache2ctl -D FOREGROUND
RUN chown -R root:www-data *
RUN chmod -R 775 *

