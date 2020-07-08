FROM nextcloud:19.0-apache
RUN sed -ri -e 's/Listen 80/Listen 8080/' \
            -e 's/Listen 443/Listen 8443/' \
            /etc/apache2/ports.conf
ENV TZ=Europe/Bucharest
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
EXPOSE 8080
