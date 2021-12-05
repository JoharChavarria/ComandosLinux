# Docker
`atp install docker` instalar docker en el equipo 

`Docker info` Permite ver los drivers de docker que se están utilizando y más información

`Docker images` Muestra todas las imágenes instaladas en el equipo 

`Docker network ls` permite ver las redes que docker ofrece 
- `Bridge` es donde arrancan todos los contenedores por defecto, creo un puente de la red local del equipo hacia el contenedor
- `Host` copia la red local del equipo en el contenedor. El contenedor y el host comparten la información de red
- `Null` Elimina toda la configuración de red del contenedor 

`sudo ifconfig docker` permite ver la configuración de la interfaz que se crea cuando se instala docker en el equipo 

`docker network create --driver (bridge/host/null) <nombre de la red>` crea una nueva red a los que los contenedores se pueden conectar 
``` 
docker network create --driver bridge testNetwork
```

`docker pull <imagen:tag>` instala una imagen en docker y le establese una etiqueta
```
docker pull alpine:lastest
```

`docker run <nombre del contenedor`inicia un contenedor 
```
docker run ubuntu
```
- `-T` se crea una terminal para el contenedor y con el parámetro i hace que la terminal sea interactiva 
- `--rm` hace que se cierra de manera automática el contenedor luego de ejecutar el último comando 
- `-d` inicia un contenedor en estado daemon.
-  `--name` le asigna un nombre específico al contenedor 

`docker ps -a` Muestra los contenedores que se están corriendo y los que no 

`docker rm <Id del contenedor>` Borra el contenedor especificado
```
docker rm 41985
```
- `-f` forzar el borrado de un contenedor corriendo


`docker stop <ID del contenedor>`detiene un contenedor
```
docker stop 17856
```

`Docker rmi <nombre de la imagen>` borra una imagen de contenedor
```
docker rmi alpine
```
- `-f` forza el borrado de la imagen en caso de que el contenedor tenga instancias corriendo 

`vim Dockerfile`Crea un archivo de dockerfile donde se pueden correr comandos adicionales para utilizar como archivo de configuración para crear nuevos contenedores

`sudo docker build -t <imagen:etiqueta> <ruta>` crea un contenedor utilizando los parámetros especificados en un dockerfile
```
sudo docker build -t curso:ubuntu .
```

## Dockerfile commands
`FROM` : obtiene la configuración de una imagen especificada 
``` 
FROM debian:9
```

`RUN` : corre cualquier comando especificado como root
``` 
RUN Echo "Hello World"
```
Se utiliza `&&` para correr más de un comando por instrucción 
```
RUN apt-get install -y nginx vim && apt-get install -y nginx vim
```

`ADD` : Añade un fichero externo del contenedor a los archivos internos del mismo
```
ADD ficheros/curso.conf/ /etc/nginx/conf.d/curso.conf
ADD ficheros/index.html /var/www/curso/index.html
```

`ENV` : Crea una variable con los valores especificados
```
ENV var1 valor1
ENV va2="hola" var3="mundo"
```

`CMD` : Hace que al iniciar un contenedor, se corra el comando especificado al igual que los parámetros. Se debe usar `[ ]` para establecer que se ejecutará un comando. El mismo se debe colocar en `“ “,` al igual que sus parámetros 
```
CMD ["uname", "-a"]
CMD ["nginx", "-g", "daemon off;"]
```

`EXPOSE <numero de puerto>` : Establece cual es el puerto que el contenedor estará utilizando. 
```
EXPOSE 80 
```
## DockerIgnore
`vim .dockerignore` crea  un archivo docker con los parámetros que serán ignorados durante la creación de un contenedor
```
vim .dockerignore
~
~
cache/
descargas/
home/jchavarriac400/
~
```
`vim docker-compose.yml`crea un archivo de docker-compose para su ejecución
```
version: '2'
services: 
        web:
           build: .
           ports: 
                  - "5000:5000"
           volumenes:
                  - .:/code
           redis:
                  imagen: "redis:alpine
 ```

## Docker Swarm
`docker-compose up` levanta la aplicación y todas las dependencias necesarias para ponerla a correr. 

`sudo docker swarm init` inicia el modo enjambre de docker 

`sudo docker service create --name nombre <imagen:etiqueta>` inicia un servicio en un contenedor 
```
sudo docker service create --name web nginx:1.10
```

`docker service scale web=#` aumenta las instancias en uso para los servicios en el swarming 
```
docker service scale web=#
```

`sudo docker service update --image <imagen:etiqueta> web` actualiza los servicios del enjambre para que obtengan la última configuración.
``` 
sudo docker service update --image nginx:1.11 web
```

`docker service rm web` borra los servicios
