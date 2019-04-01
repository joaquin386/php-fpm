FROM nginx:1.15.10
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
RUN rm /etc/nginx/conf.d/default.conf
COPY php-fpm.example.org.pem /cert.pem
COPY php-fpm.example.org.key /cert.key
COPY dhparam2048.pem /dhparam2048.pem
COPY nginx.conf /etc/nginx/
COPY php-fpm-port80.conf /etc/nginx/conf.d/
COPY php-fpm.conf /etc/nginx/conf.d/
