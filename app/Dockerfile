FROM nextcloud:18.0-apache
RUN sed -ri -e 's/Listen 80/Listen 8080/' \
            -e 's/Listen 443/Listen 8443/' \
            /etc/apache2/ports.conf
