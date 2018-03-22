FROM alpine:3.7 AS src
ENV NGINX_VERSION 1.13.10
ENV OPENSSL_VERSION 1.0.2n
RUN apk add --update \
    curl \
    gcc \
    libc-dev \
    linux-headers \
    make \
    pcre-dev \
    perl \
    zlib-dev
WORKDIR /src/openssl
ADD https://www.openssl.org/source/openssl-$OPENSSL_VERSION.tar.gz .
RUN tar -zxvf openssl-$OPENSSL_VERSION.tar.gz --strip-components 1
WORKDIR /src/nginx
ADD https://nginx.org/download/nginx-$NGINX_VERSION.tar.gz .
RUN tar -zxvf nginx-$NGINX_VERSION.tar.gz --strip-components 1
RUN ./configure \
    --prefix=/etc/nginx \
    --user=root \
    --group=wheel \
    --http-client-body-temp-path=/var/cache/nginx/client_temp \
    --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
    --with-openssl=/src/openssl \
    --with-threads \
    --with-file-aio \
    --without-http_autoindex_module \
    --without-http_browser_module \
    --without-http_empty_gif_module \
    --without-http_fastcgi_module \
    --without-http_geo_module \
    --without-http_limit_conn_module \
    --without-http_map_module \
    --without-http_memcached_module \
    --without-http_mirror_module \
    --without-http_referer_module \
    --without-http_scgi_module \
    --without-http_split_clients_module \
    --without-http_ssi_module \
    --with-http_ssl_module \
    --without-http_userid_module \
    --without-http_uwsgi_module \
    --with-http_v2_module \
    --without-mail_imap_module \
    --without-mail_pop3_module \
    --without-mail_smtp_module \
    --with-stream \
    --without-stream_geo_module \
    --without-stream_limit_conn_module \
    --without-stream_map_module \
    --without-stream_split_clients_module \
    --with-stream_ssl_module \
    --with-ld-opt='-static' \
    ${SSL_OPT}
RUN make -j1
RUN strip /src/nginx/objs/nginx

FROM scratch
COPY --from=src /src/nginx/objs/nginx /nginx
VOLUME ["/etc/nginx/conf"]
CMD ["-h"]
ENTRYPOINT ["/nginx"]
