FROM ubuntu:latest
MAINTAINER Satheeshkumar Manoharan  <infosatheesh2020@gmail.com>

#COPY ./concrete/ /usr/local/apache2/htdocs
RUN apt-get update
RUN apt-get -y upgrade

# Install apache, PHP, and supplimentary programs. curl and lynx-cur are for debugging the container.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apt-utils apache2 apache2-bin libxml2-dev curl vim unzip

# Enable apache mods.
RUN a2enmod rewrite proxy_html

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2/apache2.pid
#ENV APP_HOST $APP_HOST
#ENV APP_PORT $APP_PORT

EXPOSE 80

# Copy site into place.
#ADD ./concrete/ /var/www/html
ADD ./index.html /var/www/html/

# Update the default apache site with the config we created.
ADD ./apache-config.conf /etc/apache2/sites-enabled/000-default.conf

# By default remove old PID file if already present and simply start apache.
CMD rm -f /var/run/apache2/apache2.pid && /usr/sbin/apache2ctl -D FOREGROUND

