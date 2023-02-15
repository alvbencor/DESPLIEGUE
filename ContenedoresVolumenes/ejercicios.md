# Ejercicio 1

Dockerfile:

    FROM openjdk:11

    WORKDIR /var/www/java
    COPY ./src /var/www/java

    RUN javac Z.java
    RUN javac HolaMundo.java

    CMD ["java", "HolaMundo"]
    

Construir la imagen: 

    docker build -t alvaro/ejercicio_uno .
    

#### OJO EL PUNTO AL FINAL
    
    
Ejecutar el contenedor 

    docker run -it alvaro/ejercicio_uno
    

Ejecutar el contenedor para que se elimine al terminar 

    docker run --rm -it alvaro/ejercicio_uno
    
    
Un volumen de nombre volumen1 en el que se persistirá la información 
almacenada en la carpeta BBDD...

    docker run -it -v nombreVolumen:unbicacionInterna alvaro/ejercicio_uno
    
# Ejercicio3

Para establecer el puerto en el que escucha un servidor en Docker a través de una variable de entorno, hay que seguir los siguientes pasos:

Definir la variable de entorno: En la sección de "Environment" de su archivo Dockerfile, defina la variable de entorno que será utilizada para establecer el puerto. Por ejemplo:


    ENV PORT 8080
    
**(Solo si se necesita)** Utilizar la variable de entorno en el contenedor: En el script de inicio o en el comando que se utiliza para ejecutar el servidor en el contenedor, utilice la variable de entorno para establecer el puerto en el que el servidor escuchará. Por ejemplo:


    CMD ["python", "app.py"]


Exponer el puerto: Finalmente, en el archivo Dockerfile, especifique el puerto que se debe exponer utilizando la variable de entorno:


    EXPOSE $PORT
    
---

*Hay que cambiar en el app.listen(3000) de app.msj el número de puerto a ***(process.env.PORT)***.

Dockerfile

    FROM NODE:14
    WORKDIR /app
    COPY . .
    RUN npm install
    ENV PORT=80
    EXPOSE $PORT
    CMD ['node','app.mjs']
    
    
Ejecutar la imagen  

        docker run -p 80:80 alvaro/node-app
