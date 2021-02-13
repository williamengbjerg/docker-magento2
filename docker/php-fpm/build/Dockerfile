FROM php:7.4-fpm
WORKDIR "/application"

#Add https://github.com/mlocati/docker-php-extension-installer
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/
# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions \
        bcmath \
        gd \
        imagick \
        intl \
        pdo_mysql \
        redis \
        soap \
        zip \
        sockets \
        xsl

# https://stackoverflow.com/a/59760766/151824
RUN cd /usr/local/etc/php/conf.d/ && \
  echo 'memory_limit = -1' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer



#####################################
# wkhtmltopdf:
#####################################
#RUN apt-get update \
#    && apt-get -y --no-install-recommends install libxrender1 libfontconfig1 libx11-dev libjpeg62 libxtst6 wget \
#    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

#RUN apt-get update \
#    && curl http://security.ubuntu.com/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb --location -o /tmp/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb \
#    && apt-get --assume-yes install /tmp/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb \
#    && rm /tmp/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb \
#    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

#RUN apt-get update \
#    && curl https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb --location -o /tmp/wkhtmltox_0.12.5-1.xenial_amd64.deb \
#    && apt-get --assume-yes install /tmp/wkhtmltox_0.12.5-1.xenial_amd64.deb \
#    && rm /tmp/wkhtmltox_0.12.5-1.xenial_amd64.deb \
#    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

    #&& wget https://github.com/h4cc/wkhtmltopdf-amd64/blob/master/bin/wkhtmltopdf-amd64?raw=true -O /usr/local/bin/wkhtmltopdf \
    #&& chmod +x /usr/local/bin/wkhtmltopdf \
