FROM nginx:1.9

#ADD  nginx.conf      /etc/nginx/nginx.conf
ADD  vhost/*    /etc/nginx/conf.d/

RUN  mkdir /etc/nginx/rewrite
ADD  rewrite/*    /etc/nginx/rewrite/

#RUN  chown -R www-data.www-data /data/htdocs /data/log

VOLUME ["/data"]