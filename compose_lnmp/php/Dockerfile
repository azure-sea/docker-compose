FROM centos:7
MAINTAINER azure

ENV VERSION=5.6.31

RUN yum install -y gcc gcc-c++ make gd-devel libxml2-devel libcurl-devel libjpeg-devel libpng-devel openssl-devel && \
    yum clean all && rm -rf /var/cache/yum/*

ADD php-${VERSION}.tar.gz /tmp/

RUN cd /tmp/php-${VERSION} && \
    ./configure --prefix=/usr/local/php \
    --with-config-file-path=/usr/local/php/etc \
    --with-mysql --with-mysqli \
    --with-openssl --with-zlib --with-curl --with-gd \
    --with-jpeg-dir --with-png-dir --with-iconv \
    --enable-fpm --enable-zip --enable-mbstring && \
    make -j 4 && \
    make install && \
    cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf && \
    sed -i "s/127.0.0.1/0.0.0.0/" /usr/local/php/etc/php-fpm.conf && \
    sed -i "21a \daemonize = no" /usr/local/php/etc/php-fpm.conf
	
COPY php.ini /usr/local/php/etc/

RUN rm -rf /tmp/php-${VERSION}* && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

WORKDIR /usr/local/php
EXPOSE 9000
CMD ["./sbin/php-fpm", "-c", "/usr/local/php/etc/php.ini", "-y", "/usr/local/php/etc/php-fpm.conf"]
