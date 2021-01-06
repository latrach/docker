FROM slatrach/php8-apache:1.1

RUN apt-get update \
    && apt-get install -y libaio-dev autossh

# Oracle instantclient 
ADD https://github.com/latrach/docker/raw/main/php8-oci8-apache/instantclient/19.8.0.0.0/instantclient-basic-linux.x64-19.8.0.0.0dbru.zip /tmp/
ADD https://github.com/latrach/docker/raw/main/php8-oci8-apache/instantclient/19.8.0.0.0/instantclient-sdk-linux.x64-19.8.0.0.0dbru.zip /tmp/
ADD https://github.com/latrach/docker/raw/main/php8-oci8-apache/instantclient/19.8.0.0.0/instantclient-sqlplus-linux.x64-19.8.0.0.0dbru.zip /tmp/
ADD https://github.com/latrach/docker/raw/main/php8-oci8-apache/instantclient/19.8.0.0.0/instantclient-tools-linux.x64-19.8.0.0.0dbru.zip /tmp/

RUN unzip /tmp/instantclient-basic-linux.x64-19.8.0.0.0dbru.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-19.8.0.0.0dbru.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-19.8.0.0.0dbru.zip -d /usr/local/
RUN unzip /tmp/instantclient-tools-linux.x64-19.8.0.0.0dbru.zip -d /usr/local/

RUN ln -s /usr/local/instantclient_12_2 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.12.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus

RUN echo 'export LD_LIBRARY_PATH="/usr/local/instantclient"' >> /root/.bashrc

RUN echo 'umask 002' >> /root/.bashrc

RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8
RUN echo "extension=oci8.so" > /usr/local/etc/php/conf.d/php-oci8.ini

RUN rm /tmp/instantclient-basic-linux.x64-19.8.0.0.0dbru.zip
RUN rm /tmp/instantclient-sdk-linux.x64-19.8.0.0.0dbru.zip
RUN rm /tmp/instantclient-sqlplus-linux.x64-19.8.0.0.0dbru.zip
RUN rm /tmp/instantclient-tools-linux.x64-19.8.0.0.0dbru.zip

WORKDIR /var/www/
