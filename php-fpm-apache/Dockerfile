ARG PHP_TAG
FROM srijanlabs/php-fpm:${PHP_TAG}

USER root
RUN DEBIAN_FRONTEND=noninteractive apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    apache2 \
    libapache2-mod-fcgid \
    && a2enmod actions \
    && a2enmod proxy \
    && a2enmod rewrite \
    && a2enmod proxy_fcgi \
    && rm -rf /var/lib/apt/lists/*

COPY start.sh /usr/local/bin/start.sh

# Apache configurations
COPY app.conf /etc/apache2/sites-enabled/000-default.conf
COPY envvars ports.conf /etc/apache2/

ENV DOC_ROOT "/app/web"

EXPOSE 8080

ENV PATH="/app/web/vendor/bin:${PATH}" \
    USER_GROUP="continua:continua" \
    PHP_HOST=localhost

RUN mkdir /var/run/{apache2,fpm} \
    && chmod -R 0777 /var/tmp \
    && chown -R ${USER_GROUP} /var/{log,run/{fpm,apache2},lib/apache2} \
    && chown -R ${USER_GROUP} /etc/apache2

USER continua

CMD [ "start.sh" ]
