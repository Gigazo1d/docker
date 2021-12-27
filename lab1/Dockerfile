FROM debian:bullseye

COPY bullseye_repo.list /etc/apt/sources.list.d/

RUN apt update && apt install -y && \
apt install -y nginx && \
apt autoclean

RUN rm -R /var/www/* && mkdir -p \
/var/www/prod.local && mkdir -p \
/var/www/prod.local/img

COPY index.html /var/www/prod.local 

COPY kong.jpg /var/www/prod.local/img

RUN chmod -R 755 /var/www/prod.local

RUN useradd evgeny && \
groupadd kukushin && \
usermod -a -G kukushin evgeny && \
chown -R evgeny:kukushin /var/www/prod.local

RUN sed -i 's/html/prod.local/g' /etc/nginx/sites-available/default

RUN sed -i 's/index.htm/index.html/g' /etc/nginx/sites-available/default

RUN sed -i 's/www-data/evgeny kukushin/g' /etc/nginx/nginx.conf

CMD ["nginx", "-g", "daemon off;"]
