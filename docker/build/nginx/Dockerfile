FROM nginx

ENV \
  HOME /root \
  DEBIAN_FRONTEND noninteractive

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

ADD ./default /etc/nginx/conf.d/default.conf

EXPOSE 80 443

CMD service nginx start