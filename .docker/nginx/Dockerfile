FROM nginx:latest

# RUN set -x \
#     && apt-get update && apt-get install --no-install-recommends -yqq \
# dnsmasq
# Add the nginx configuration file to the container
RUN rm /etc/nginx/conf.d/default.conf
ADD nginx.tmpl /etc/nginx/conf.d/default.conf
ADD letsencrypt.conf /etc/nginx/snippets/letsencrypt.conf
ADD ssl.conf /etc/nginx/snippets/ssl.conf
ADD php.conf /etc/nginx/snippets/php.conf
ADD server_default.conf /etc/nginx/snippets/server_default.conf

RUN mkdir -p /srv/config

ADD start.sh /srv/config/start.sh
ADD reload.sh /srv/config/reload.sh
RUN chmod +x /srv/config/start.sh /srv/config/reload.sh

RUN usermod -a -G www-data nginx
# RUN sed -i 's/nginx;/www-data/g' /etc/nginx/;

ENTRYPOINT ["/bin/bash", "/srv/config/start.sh"]
CMD ["nginx", "-g", "daemon off;"]
