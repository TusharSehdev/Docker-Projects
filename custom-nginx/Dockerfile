FROM alpine:latest


EXPOSE 80

ARG FILENAME="nginx-1.19.2"
ARG EXTENSION="tar.gz"

RUN apk add --no-cache pcre zlib openssl && \
    apk add --no-cache \
            --virtual .build-deps \
            build-base \
            pcre-dev \
            zlib-dev \
            openssl-dev && \

    wget https://nginx.org/download/${FILENAME}.${EXTENSION} && \
    tar -xvf ${FILENAME}.${EXTENSION} && \
    rm ${FILENAME}.${EXTENSION} && \

    cd ${FILENAME} && \
    ./configure \
        --sbin-path=/usr/bin/nginx \
        --conf-path=/etc/nginx/nginx.conf \
        --error-log-path=/var/log/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --with-pcre \
        --pid-path=/var/run/nginx.pid \
        --with-http_ssl_module && \
    make && make install && \
    cd / && \

    rm -rf ${FILENAME} && \
    apk del .build-deps

CMD ["nginx", "-g", "daemon off;"]
