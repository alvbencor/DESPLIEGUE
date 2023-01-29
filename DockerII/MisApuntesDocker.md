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

La primera línea, **"FROM node:14"**, indica que esta imagen se basará en la imagen oficial de Node.js versión 14. Esto significa que la imagen resultante tendrá Node.js ya instalado en ella.

La segunda línea, **"WORKDIR /app"**, establece el directorio de trabajo en el contenedor en "/app". Todos los comandos subsecuentes se ejecutarán en este directorio.

La tercera línea, **"COPY . ."**, copia todos los archivos del directorio actual en el host al directorio de trabajo en el contenedor.

La cuarta línea, **"RUN npm install"**, ejecuta el comando "npm install" en el contenedor. Esto instalará todas las dependencias de la aplicación Node.js especificadas en el archivo package.json.

La quinta línea, **"EXPOSE 3000"**, indica al contenedor que debe escuchar en el puerto 3000. Esto permite que otros contenedores o el host conecten a la aplicación Node.js en ese puerto.

La sexta línea, **"CMD [ "node", "app.mjs"]"**, especifica el comando que se ejecutará cuando se inicie el contenedor. En este caso, se ejecutará el archivo "app.mjs" usando el comando "node".

## Diferencia entre las instrucciones RUN y CMD

**RUN** se ejecuta al construir una imagen para realizar una acción, creando una capa nueva.

**CMD** se encarga de pasar valores predeterminados a un contenedor, los cuales se ejecutaran cuando el contenedor se inicialice. Sólo de be haber una instucción CDM en un Dockerfile, y si hay más, sólo se ejecutará el último.


### **docker attach

Este comando permite, indicando un contenedor concreto, vincular la entrada y salida de errores estándar del mismo, al terminal que se ejecute.  Se tiene que introducir el **id o el nombre a vincular**. Cuando se ejecuta un contenedor sin la opcion d, el contenedor se ejecuta por defecto en **modo vinculado**.

### **docker logs**

Para ver los logs que se han imprimido de un contenedor en concreto. Se indica su nombre o el id. Con la opcion -f se puede activar el modo seguimiento de logs.


### **docker run -it

En el caso de que una aplicación no sea accesible a traves del navegador al ejecutar un contenedor en concreto, se podrá ver en consola su ejecución pero no interactuar con ella.

Con la opción **-i** se mantiene el canal de entrada (stdin) del contenedor, abriendo el contenedor en modo interactivo.

Con la opción **-t** se asocia una **tty** (terminal).

Es posible incluir las dos opciones como **-it**

Esto sirve para aplicaciones de consola.

### **docker run -rm**

Con esta opción se elimina el contenedor después de ejecutarse. El contenedor no pasará de ejecución a parado, sino que desaparecerá.

### **docker image inspect**

Con este comando se obtiene información de la imagen, como las capas q conforman la imagen (las suyas y las de la imagen base), configuración para los futuros contenedores que se ejecuten a partir de ella, sistema operativo de la imagen, etc..

### **docker tag**

Permite renombrar una imagen. Si se quiere subir una imagen ya creada a un repositorio, pero u nombre no coincide con el del repo, se puede modificar ese nombre con el comando 

        docker tag nombreAntiguo nombreNuevo

Es posible incluir la etiqueta de la misma forma que se ha visto hasta el momento:

        docker tag nombreAntiguo:tag nombreNuevo:tag

Este renombre es más bien una clonación. Se creará una nueva imagen, exacta a la anterior con un nombre diferente. 





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
