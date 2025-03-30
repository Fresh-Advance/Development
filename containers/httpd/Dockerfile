FROM httpd:2.4-alpine

COPY custom.conf /usr/local/apache2/conf/custom.conf
COPY project.conf /usr/local/apache2/conf/project.conf

COPY certs/server.crt /usr/local/apache2/conf/server.crt
COPY certs/server.key /usr/local/apache2/conf/server.key

RUN printf "Include conf/custom.conf\n" >> /usr/local/apache2/conf/httpd.conf && \
    printf "Include conf/project.conf" >> /usr/local/apache2/conf/httpd.conf

RUN sed -i \
    -e 's/^#\(Include .*httpd-ssl.conf\)/\1/' \
    -e 's/^#\(LoadModule .*mod_ssl.so\)/\1/' \
    -e 's/^#\(LoadModule .*mod_socache_shmcb.so\)/\1/' \
    /usr/local/apache2/conf/httpd.conf