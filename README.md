# Configuración docker proyecto en Codeigniter 4

Este proyecto tiene como objetivo configurar un entorno de desarrollo para un proyecto en Codeigniter 4 con docker. 

<!-- Indice -->
## Índice
- [Configuración docker proyecto en Codeigniter 4](#configuración-docker-proyecto-en-codeigniter-4)
  - [Índice](#índice)
  - [Requisitos](#requisitos)
  - [Configuración](#configuración)
  - [Acceder a los servicios](#acceder-a-los-servicios)


## Requisitos
- Tener instalado docker y docker-compose

## Configuración
1. Clonar el repositorio

```bash
    git clone <url-repositorio>
```

2. Crear el archivo .env

```bash
    cp .env.example .env
```

3. Configurar el archivo .env

```bash
# General
PROJECT_NAME=project_name

# Database
DB_USER=root
DB_PASSWORD=123456
DB_ROOT_PASSWORD=123456

# Puertos de los servicios
APACHE_PORT=80
PHPMYADMIN_PORT=8080
MARIADB_PORT=3306
```

4. Crear el volumen de la base de datos **con el nombre del proyecto y el sufijo -vol**

```bash
    docker volume create --name=project_name-vol
```

5. Mover la carpeta de configuración de docker a la raíz del proyecto de modo que quede de la siguiente manera:

```bash
    .
    ├── app
    ├── docker
    ├── public
    ├── system
    ├── tests
    ├── writable
    ├── .env
    ├── composer.json
    ├── composer.lock
    ├── spark
    └── spark.bat
```

6. Navegar a la carpeta docker y ejecutar el siguiente comando

```bash
    docker-compose up -d
```

7. Ejecutar composer install

```bash
    docker-compose exec app composer install
```

8. Ejecutar las migraciones

```bash
    docker-compose exec app php spark migrate
```

9. Ejecutar el seeder

```bash
    docker-compose exec app php spark db:seed
```

## Acceder a los servicios
Una vez que los servicios estén corriendo, se puede acceder a ellos de la siguiente manera: 

- **App**: http://localhost:80
- **PhpMyAdmin**: http://localhost:8080
- **Base de datos**: localhost:3306

Teniendo en cuenta que los puertos pueden variar dependiendo de la configuración del archivo .env
