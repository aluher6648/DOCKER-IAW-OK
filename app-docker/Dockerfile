FROM php:7.4-apache

# Instala el cliente de MariaDB
RUN apt-get update && apt-get install -y mariadb-client

# Instala extensiones PHP necesarias
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli


# Copia el código de la aplicación al contenedor
ADD bookmedik /var/www/html/

# Cambiar los permisos del directorio /var/www/html/ y sus contenidos
RUN chmod -R 755 /var/www/html/

# Exponer el puerto 80 para tráfico web
EXPOSE 80

# Configura las variables de entorno para la conexión a la base de datos
ENV DB_HOST=mariadb
ENV DB_PORT=3306
ENV DB_DBNAME=bookmedik
ENV DB_USER=root
ENV DB_PASS=dbpass

# Copia el archivo script.sh al directorio /usr/local/bin dentro del contenedor
ADD  script.sh /usr/local/bin/script.sh

# Cambia los permisos del archivo script.sh para que sea ejecutable
RUN chmod +x /usr/local/bin/script.sh

# Copia el archivo schema.sql al directorio /opt dentro del contenedor
ADD bookmedik/schema.sql /opt

# Cambiar los permisos del directorio /opt/schema.sql y sus contenidos
RUN chmod -R 755 /opt/schema.sql

# Inicializa la base de datos con schema.sql y ejecuta Apache
CMD /usr/local/bin/script.sh
