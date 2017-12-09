FROM nginx:alpine

ENV \
  HOME /root \
  DEBIAN_FRONTEND noninteractive

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN echo "upstream fastcgi_backend { server phpfpm:9000; }" > /etc/nginx/conf.d/upstream.conf

ADD ./default /etc/nginx/conf.d/default.conf

EXPOSE 80 443

CMD service nginx start