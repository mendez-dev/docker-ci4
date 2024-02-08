FROM php:7.4-apache

# Habilitar extensiones necesarias
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

# Actualizar y mejorar
RUN apt-get update && apt-get upgrade -y

# instalar dependencias de codeigniter 4 (ext-intl, ext-gd, ext-zip)
RUN apt-get install -y libicu-dev libpng-dev libzip-dev
RUN docker-php-ext-install intl gd zip


# Habilitar mod_rewrite
RUN a2enmod rewrite

# modificar php.ini para aumentar el tamaño de carga a 100MB
RUN echo "upload_max_filesize = 100M" > /usr/local/etc/php/conf.d/uploads.ini
RUN echo "post_max_size = 100M" >> /usr/local/etc/php/conf.d/uploads.ini

# Instalar git
RUN apt-get install -y git

# Instalar composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'edb40769019ccf227279e3bdd1f5b2e9950eb000c3233ee85148944e555d97be3ea4f40c3c2fe73b22f875385f6a5155') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

# Copiar archivo de configuración de apache
COPY ./php/000-default.conf /etc/apache2/sites-available/000-default.conf

# Reiniciar apache
RUN service apache2 restart
