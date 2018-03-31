# Estamos extendiendo una imagen oficial de Docker Hub

FROM nginx:1.13
# Latest se recomienda si estas aprendiendo o desarrollando. Si es produccion, es buena practica especificar la version.

WORKDIR /usr/share/nginx/html
# Cambia el directorio de trabajo de / al webhost de nginx
# Usar WORKDIR es mejor a usar 'RUN cd /some/path'

COPY index.html index.html

# No se tiene que especificar EXPOSE o CMD porque vienen del FROM
