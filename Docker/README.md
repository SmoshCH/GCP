<img src="image.png" alt="Docker" style="display: block; margin: 0 auto;"> <br>

# Docker 

## Que es Docker? 
Es una plataforma que permite crear, ejecutar y gestionar aplicaciones en contendores.<br>

## What is Docker?
Is a Platform that allows to create, execute and manage applications in containers.<br>

## Links importantes 
[Instalar docker](https://www.youtube.com/watch?v=jiJFDwmWrWk&ab_channel=UskoKruM2010)<br> 
[Docker desktop](https://www.docker.com/products/docker-desktop/)<br>
[Instalacion](https://docs-docker-com.translate.goog/desktop/setup/install/windows-install/?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=tc)<br>
[Aprender docker](https://www.youtube.com/watch?v=4Dko5W96WHg&ab_channel=HolaMundo)<br>
[WLS for windows](https://learn.microsoft.com/es-es/windows/wsl/install)<br>
[Docker hub](https://hub.docker.com/)<br>


## Instalación de docker desktop en windows
- Tener virtualizacion de bios activada [(video)](https://www.youtube.com/watch?v=tgH4_jkiMbc&ab_channel=EmuladoresdeAndroid) <br>
- Instalar WLS [link](https://learn.microsoft.com/es-es/windows/wsl/install) <br>
- Ejecutar como administrador powershell (azul)
- Ejecutar en consola de powershel > wsl --install <br>
- Iniciar ubuntu shell > crear usuario > crear contraseña <br>
- Instalar instalador de docker [link](https://docs-docker-com.translate.goog/desktop/setup/install/windows-install/?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=tc) <br>
- Fin. <br>

## Docker cheatsheet

### Docker comandos rápidos
| Comando                        | Descripción                                   | 
|--------------------------------|-----------------------------------------------|
| `docker images -a`             | Muestra la versión más corta.                 |
| `docker pull mongo`            | Descarga imagen.                              | 
| `docker image rm mongo1`       | Elimina imagen llamada mongo1.                | 
| `docker create --name m mongo` | Crea contenedor con nombre m y imagen mongo.  |
| `docker rm m`                  | Elimina contenedor llamado m.                 | 
| `docker start m`               | Inicia contenedor m.                          |
| `docker down m`                | Apaga contenedor m.                           |
| `docker create --name m mongo` | Crea contenedor con nombre m y imagen mongo.  |
| `docker run --name m -p27017:27017 -d mongo` | Crea contenedor nombra e inicia.  | 
| `docker network ls`            | Lista las redes creadas.                      |
| `docker network create mired`  | Crea red mired.                               |
| `docker network rm mired`      | Elimina red mired.                            |
| `docker build -t miapp:1`      | Crea contenedor desde documento y lo llama miapp.|





docker version > muestra la version de dockert
docker --version > Muestra la versión mas corta 
docker images > muestra imagenes descargadas
docker pull node > descarga imagen  
docker pull node:18 (imagen mas version 18)
docker image rm nombreimage > eliminar imagenes
docker image rm node:18, node, mysql etc 
docker create mongo > crea contenedor en base a nuestra imagen ya guardada
f0a65f01205b2bdcefbd2139fd87bbb734af9dc0a0b1755e8fd9c8a4b5d8549f (identificador de container)
docker container create mongo > crea contenedor pero forma mas larga 
docker start f0a65f01205b2bdcefbd2139fd87bbb734af9dc0a0b1755e8fd9c8a4b5d8549f >ejecutar contenedor 
docker ps > verificar contenedor creado 
f0a65f01205b (id corto del contenedor)
docker stop f0a65f01205b > detener contenedor 
docker ps -a > ver contenedores creados
docker rm pensive_feynman > eliminar contenedor con id o nombre 
docker create --name monguito mongo > nombrar contendores, con el nombre sgeguido de  el nombre de imagen 
mapear puerto 
docker create -p27017:27017 --name monguito mongo
-p es de publish primer puerto es de nuestra maquina y segundo de docker 
docker create -p27017 --name monguito mongo (deja que docker decida el puerto del host, no recomendable)
verificar servidor de mongo 
docker logs monguito ve los logs del servidor 
docker logs --follow monguito >sigue esuchando los puertos para ver si hay mas logs
docker run (crea imagen, crea contenedor y lo inicia)
docker run --name monguito -p27017:27017 -d mongo
variables de entorno 
docker create -p27017:27017 --name monguito -e MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo
e- es variable de entorno 

meter app a docker 
crear archivo dockerfile 
FROM node:18 

RUN mkdir -p /home/app 
COPY . /home/app

EXPOSE 3000

CMD ["node", "/home/app/index.js"]

conectar contenedores en 1 red 
docker network ls > ve las redes creadas
docker network create mired
docker network rd mired

crear imagenes en base a archivo dockerfile

docker build -t miapp:1 .
-t escribir nombre de el contenedor 


crear contendor en red 
docker create -p27017:27017 --name monguito --network mired -e MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo

crear imagen
crear red
crear contenedor >asignar puertos >asignar nombre >variables de entorno >especificar red >indicar imagen:etiqueta 
automatizar con docker compose

docker compose
crear documento con 
docker-compose.yml 

version: "3.9"
services: 
	chanchito: 
		build: .
		ports:
			- "3000:3000"
		links: 
			- monguito
	monguito:
		image: mongo
		ports: 
			- "27017:27017"
		environment: 
			- MONGO_INITDB_ROOT_USERNAME=nico
			- MONGO_INITDB_ROOT_PASSWORD=password 



docker compose up > inicia docker compose el documento
control c detine docker compose 
docker compose down > elimina todos los archivos creados

volumenes 
no eliminan la data de ellos 
en archivo de  docker compose 

	volumes: 
		-mongo-data:/data/db

volumes: 
	mongo-data: 

41:23
