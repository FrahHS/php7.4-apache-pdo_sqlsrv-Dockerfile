FROM php:7.4-apache-buster

RUN apt-get update
RUN apt-get install -y apt-utils gnupg curl software-properties-common

# apache 2 settings
RUN a2enmod rewrite
RUN service apache2 restart

# Microsoft ODBC 17 Driver
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get -y install msodbcsql17
RUN apt-get -y install unixodbc-dev libxml2-dev

# sqlsrv pdo extension
RUN pecl install sqlsrv
RUN pecl install pdo_sqlsrv
RUN printf "; priority=30\nextension=sqlsrv.so\n" > /usr/local/etc/php/conf.d/sqlsrv.ini
RUN printf "; priority=40\nextension=pdo_sqlsrv.so\n" > /usr/local/etc/php/conf.d/pdo_sqlsrv.ini

# Others dependencies
RUN docker-php-ext-install gettext 
