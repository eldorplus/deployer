FROM nginx

ENV \
  HOME /root \
  DEBIAN_FRONTEND noninteractive

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

ADD ./app.conf /etc/nginx/conf.d/

EXPOSE 80 443

CMD service nginx start