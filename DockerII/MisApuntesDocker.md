## Docker



## Cómo crear una imagen de una aplicación Node.js

    package.json:
    ---
    
    {
      "name": "mi-nodejs-server",
      "version": "1.0",
      "main": "server.js",
      "dependencies": {
        "express": "^4.17.1",
        "body-parser": "1.19.0"
      }
    }


Archivo Dockerfile:



    Dockerfile:
    ---

    FROM node:14

    WORKDIR /app

    COPY . .

    RUN npm install

    EXPOSE 3000

    CMD [ "node", "app.mjs"]


Este archivo Dockerfile es un ejemplo de cómo crear una imagen de una aplicación Node.js.

La primera línea, "FROM node:14", indica que esta imagen se basará en la imagen oficial de Node.js versión 14. Esto significa que la imagen resultante tendrá Node.js ya instalado en ella.

La segunda línea, "WORKDIR /app", establece el directorio de trabajo en el contenedor en "/app". Todos los comandos subsecuentes se ejecutarán en este directorio.

La tercera línea, "COPY . .", copia todos los archivos del directorio actual en el host al directorio de trabajo en el contenedor.

La cuarta línea, "RUN npm install", ejecuta el comando "npm install" en el contenedor. Esto instalará todas las dependencias de la aplicación Node.js especificadas en el archivo package.json.

La quinta línea, "EXPOSE 3000", indica al contenedor que debe escuchar en el puerto 3000. Esto permite que otros contenedores o el host conecten a la aplicación Node.js en ese puerto.

La sexta línea, "CMD [ "node", "app.mjs"]", especifica el comando que se ejecutará cuando se inicie el contenedor. En este caso, se ejecutará el archivo "app.mjs" usando el comando "node".



## Crear una imagen a partir de un dockerfile

        docker build -t nombre_de_la_imagen .
        
*El nombre de la imagen siempre en minusculas. 
***-t*** añade la etiqueta

Ejercicio2: docker build -t alvaro/ejercicio2b .



## Ejecutar 

        docker run -p 80:80 nombre_de_la_imagen
        

Ejercicio 2: docker run -p 80:80 alvaro/ejercicio2b




## Como instalar Docker en ubuntu server sobre virtualbox

Actualice la lista de paquetes ejecutando el comando: 

        sudo apt-get update
        
        
Instale Docker ejecutando el comando: 

        sudo apt-get install docker.io -y
        
Inicie el servicio de Docker ejecutando el comando: 

        sudo systemctl start docker
        
Verifique que Docker se está ejecutando correctamente ejecutando el comando: 

        sudo docker run hello-world
        
        

## Instalar Visual Studio Code en Ubuntu

    sudo snap install --classic code
