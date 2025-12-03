FROM mariadb:10.11

ENV MYSQL_ROOT_PASSWORD=root123
ENV MYSQL_DATABASE=accounts
ENV MYSQL_USER=admin
ENV MYSQL_PASSWORD=admin123

COPY init.sql /docker-entrypoint-initdb.d/01-init.sql

EXPOSE 3306
