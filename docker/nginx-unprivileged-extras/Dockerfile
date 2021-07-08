FROM nginxinc/nginx-unprivileged:1.18 as builder

# module version
ENV MODULE_TAG v0.33
ENV MODULEDIR /tmp/headers-more-nginx-module

# switch to root to compile extras
USER root

RUN set -x && \
    NGINX_VERSION=$(nginx -v 2>&1 | cut -f2 -d/) && \
    echo "deb-src https://nginx.org/packages/debian/ buster nginx" >> /etc/apt/sources.list.d/nginx.list && \
    apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y git wget && \
    wget "http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz" -O nginx.tar.gz && \
    git clone --depth 1 --branch ${MODULE_TAG} https://github.com/openresty/headers-more-nginx-module ${MODULEDIR} && \
    apt-get build-dep -y nginx=${NGINX_VERSION}-${PKG_RELEASE} && \
    tar -zxC /usr/src -f nginx.tar.gz && \
    rm -rf nginx.tar.gz  && \
    cd /usr/src/nginx-$NGINX_VERSION && \
    ./configure --with-compat $CONFARGS --add-dynamic-module=${MODULEDIR} && \
    make && make install

FROM nginxinc/nginx-unprivileged:1.18

#switch to root to install modules
USER root

COPY --from=builder /usr/local/nginx/modules/ngx_http_headers_more_filter_module.so /usr/lib/nginx/modules/
RUN sed -i '/^worker_processes  1;/a load_module /usr/lib/nginx/modules/ngx_http_headers_more_filter_module.so;' /etc/nginx/nginx.conf && \
    chown -R 101:0 /etc/nginx

# switch back to unprivileged user
USER 101