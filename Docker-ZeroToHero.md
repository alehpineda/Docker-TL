# Docker - Zero to Hero

## By M. C. Alejandro H. Pineda 
### From CIINN - Centro de Innovacion Acelerada A. C. and Coders Link.

## Docker Setup

### Links para instalacion 

[Instrucciones Generales](https://docs.docker.com/install/)

[Edicion Community](https://www.docker.com/community-edition)

[Instalacion para Raspberry Pi](https://www.raspberrypi.org/blog/docker-comes-to-raspberry-pi/)

[Play with docker](https://labs.play-with-docker.com)

Se requiere registro [previo](https://hub.docker.com)

### Docker docs

[Tu mejor aliado](https://docs.docker.com)

### Checar instalacion y hola mundo.

```bash
# Muestra info sobre la instalacion docker
docker info
# Hola mundo desde docker
docker container run hello-world
```

## Crear y usar contenedores "Like a Boss"

```bash
docker container run nginx 
# corre nuevo contenedor nginx

docker container run -d httpd
# corre nuevo contenedor apache en modo detach

docker container ps
docker ps
# Muestra el listado de los contenedores corriendo.

docker container ps
# Muestra el listado de los contenedores corriendo.

docker container stop <nombre del contenedor> 
# detiene contenedor usando id o nombre

docker container start <nombre del contenedor> 
# Inicia un contenedor usando id o nombre previamente detenido

docker container rm <id del contenedor> 
# remueve/elimina contenedor usando id o nombre

docker container run -p 8080:80 --name apache -d httpd 
# Correr nuevo contenedor httpd con nombre "apache" en detach en el puerto 8080 del host

docker container run -p 8888:80 --name nginx -d nginx 
# Correr nuevo contenedor nginx con nombre "nginx" en detach en el puerto 8080 del host

docker logs apache
# Muestra los logs del contenedor llamado "apache", puedes usar id o nombre del contenedor.

docker top nginx
# Comando top en contenedor llamado "nginx"

docker pull python
# Descarga imagen python, default latest

docker container run -it --name proxy nginx bash 
# Iniciar nuevo contenedor nginx con nombre proxy de manera interactiva con terminal e inicialice bash.

docker container run -it --name ubuntu ubuntu 
# Iniciar nuevo contenedor ubuntu con nombre ubuntu de manera interactiva

docker container start -ai ubuntu 
# Reinicia contenedor interactivo de ubuntu

docker container exec -it nginx bash 
# Exec corre un proceso extra al contenedor previamente creado y corriendo. Contenedor interactivo de nginx con bash.

docker container port nginx
# Muestra los puertos del contenedor llamado "nginx"

docker network ls 
# listar redes

docker network inspect <nombre de red>
# Inspeccionar una red

docker network create --driver <tipo de driver, default=bridge>
# crear una red

docker network connect <nombre de red> <nombre contenedor>
# Conectar una red a un contenedor

docker network disconnect <nombre de red> <nombre contenedor>
# Desconectar una red de un contenedor

docker container run -d --network mi_red --name nuevo_nginx -p 8080:80 nginx 
# Iniciar nuevo contenedor nginx llamado nuevo_nginx en la red mi_red. Previamente creada la red.

docker container run -d --network my_app_net --network mi_red --name nuevo_apache -p 8888:80 apache
# Iniciar nuevo contenedor apache llamado nuevo_apache en la red mi_red y my_app_net. Previamente creadas las redes.

docker container prune
# Eliminar todas las redes que no esten unidas a contenedores
```

## Imagenes de contenedores, donde encontrarlas y como construirlas.

### Docker hub

[Docker hub](https://hub.docker.com)

```bash
docker pull <nombre de la imagen>:<version>
# Descarga la imagen especificada, default latest.

docker images
# Lista todas las imagenes instaladas

docker history nginx 
# Checar la historia de la imagen nginx

docker image inspect nginx 
# Checar metadatos de la imagen nginx

docker image build -t customnginx . 
# Construir imagen llamada customnginx usando el Dockerfile de la carpeta dockerfile-1

docker rmi <nombre imagen>
# Eliminar imagen
```

### Construir una imagen

```bash
docker image build -t nginx_html . 
# Construir image llamada nginx_html usando el Dockerfile del archivo. dockerfile-2

docker container run -d -p 80:80 --name mi_pagina nginx_html
# Correr un contenedor nginx_html en modo detach con puertos 80 y nombre mi_pagina 

docker image tag nginx_html:latest deathscythe/nginx_html:latest 
# Taguear imagen con mi login de docker hub para despues empujarla.

docker push <usuarioDockerHub>/nginx_html:latest 
# Empujar imagen nginx_html:latest a mi repositorio en docker hub. Preguntara por credenciales.

docker rmi <usuarioDockerHub>/nginx_html:latest 
# Eliminar imagen

docker pull <usuarioDockerHub>/nginx_html:latest 
# Descargar imagen
```

## Volumenes. La vida del contenedor y como persistir datos.

### Volumenes

Existen tres tipos de volumenes

- Anonimo
  - solo tiene direccion dentro de la imagen
- Nombre
  - Tiene un nombre amigable para ser encontrado dentro de la imagen
- Host
  - tiene direccion dentro del host que esta reflejada en la imagen. Cambios hechos en el host se hacen en la imagen.

```bash
docker volume prune 
# Eliminar volumenes no ligados a un contenedor

docker volume ls 
# Listar los volumenes

docker volume create <nombre del volumen>
# Crear un volumen con diferentes drivers y tags antes de hacer docker container run

docker volume inspect <nombre del volumen>
# inspeccionar los volumenes

docker container run -d --name mysqltest -e MYSQL_ALLOW_EMPTY_PASSWORD=Yes -v mysql-db:/var/lib/mysql mysql 
# Iniciar nuevo contenedor de mysql con nombre mysqltest y variable MYSQL_ALLOW_EMPTY_PASSWORD=Yes y volumen llamado mysql-db ligado a /var/lib/mysql.

docker container run -d --name postgres9.6.1 -v psql-data:/var/lib/postgresql/data postgres:9.6.1
# Correr un contenedor postgre en detach con un volumen llamado psql-data.

docker logs postgres9.6.1
# Ver los logs del contenedor

docker container run -d --name postgres9.6.2 -v psql-data:/var/lib/postgresql/data postgres:9.6.2
# Correr un contenedor postgre en detach con un volumen llamado psql-data, actualizado.

docker logs postgres9.6.2
# Ver los logs del contenedor

docker logs -f postgres9.6.1 
# Follow -f para seguir los logs

docker logs -f postgres9.6.2 
# Follow -f para seguir los logs

```

## Docker Compose, la herramienta de multi-contenedores.

### Docker Compose

```bash 
docker-compose up 
# Inicia el servicio compose, tiene que existir un archivo docker-compose.yml

docker-compose down
# Tira el servicio compose.

docker-compose -f <archivoCompose> up -d
# Elige el archivo compose a utilizar

docker-compose logs
# Muestra los logs del compose.
```

