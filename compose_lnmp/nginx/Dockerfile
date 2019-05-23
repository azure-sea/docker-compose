FROM centos:7
MAINTAINER azure

#ENV VERSION=1.12.1
ENV VERSION=1.14.2

RUN yum install -y gcc gcc-c++ make openssl-devel pcre-devel && \
    yum clean all && rm -rf /var/cache/yum/*

ADD nginx-${VERSION}.tar.gz /tmp

RUN cd /tmp/nginx-${VERSION} && \
    ./configure --prefix=/usr/local/nginx \
	--with-http_ssl_module \
    --with-http_stub_status_module && \
    make -j 2 && \
    make install

RUN rm -rf /tmp/nginx-${VERSION}* && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ENV PATH $PATH:/usr/local/nginx/sbin

COPY nginx.conf /usr/local/nginx/conf/nginx.conf

WORKDIR /usr/local/nginx

EXPOSE 80
CMD ["./sbin/nginx", "-g", "daemon off;"]
