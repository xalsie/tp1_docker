# <!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#  PHP-FPM 8.1.0 Dockerfile - PHP 8.1
# 
#  #  Developed by    : LeGrizzly#0341
#  #  Support         : LeGrizzly#0341
#  #  GitHub          : https://github.com/xalsie
#   _                _____          _               _         
#  | |              / ____|        (_)             | |        
#  | |        ___  | |  __   _ __   _   ____  ____ | |  _   _ 
#  | |       / _ \ | | |_ | | \__| | | |_  / |_  / | | | | | |
#  | |____  |  __/ | |__| | | |    | |  / /   / /  | | | |_| |
#  |______|  \___|  \_____| |_|    |_| /___| /___| |_|  \__, |
#                                                        __/ |
#                                                       |___/
#  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~_Update: 16/05/23_~~-->
FROM alpine:3.17.3

RUN apk --no-cache --repository https://dl-cdn.alpinelinux.org/alpine/edge/testing add \
    # install necessary PHP packages
    tini \
    # php81 \
    php81-pgsql \
    php81-pdo_pgsql \
    php81-session \
    php81-fpm && \
    ln -sf /usr/bin/php81 /usr/bin/php && \
    rm -rf /var/cache/apk/*

# ensure www-data user exists
RUN  adduser -u 82 -D -S -G www-data www-data

# FIX volume Permission denied
RUN mkdir -p /var/www/html && chown -R www-data:www-data /var/www/html && chmod 755 /var/www/html

# FIX showlog Permission denied
RUN mkdir -p /var/log && chmod 777 /var/log

ADD rootfs /

ENTRYPOINT ["/sbin/tini", "--"]

EXPOSE 9000

USER www-data

WORKDIR /var/www

CMD ["php-fpm81", "--nodaemonize"]
