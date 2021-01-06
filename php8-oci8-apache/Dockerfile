FROM slatrach/php8-apache:1.1

RUN apt-get update \
    && apt-get install -y libaio-dev autossh

# Oracle instantclient 
ADD https://download.oracle.com/otn_software/linux/instantclient/211000/instantclient-basic-linux.x64-21.1.0.0.0.zip /tmp/
ADD https://download.oracle.com/otn_software/linux/instantclient/211000/instantclient-sdk-linux.x64-21.1.0.0.0.zip /tmp/
ADD https://download.oracle.com/otn_software/linux/instantclient/211000/instantclient-sqlplus-linux.x64-21.1.0.0.0.zip /tmp/

RUN unzip /tmp/instantclient-basic-linux.x64-21.1.0.0.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-21.1.0.0.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-21.1.0.0.0.zip -d /usr/local/

RUN ln -s /usr/local/instantclient_21_1 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus
RUN sh -c "echo /usr/local/instantclient > /etc/ld.so.conf.d/oracle-instantclient.conf"
RUN ldconfig
RUN echo 'export LD_LIBRARY_PATH="/usr/local/instantclient"' >> /root/.bashrc
RUN echo 'umask 002' >> /root/.bashrc
RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8
RUN echo "extension=oci8.so" > /usr/local/etc/php/conf.d/php-oci8.ini

RUN rm /tmp/instantclient-basic-linux.x64-21.1.0.0.0.zip
RUN rm /tmp/instantclient-sdk-linux.x64-21.1.0.0.0.zip 
RUN rm /tmp/instantclient-sqlplus-linux.x64-21.1.0.0.0.zip

WORKDIR /var/www/
