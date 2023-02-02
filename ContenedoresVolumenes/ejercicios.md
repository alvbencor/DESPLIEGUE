# Ejercicio 1

Dockerfile:

    FROM openjdk:11

    WORKDIR /var/www/java
    COPY ./src /var/www/java

    RUN javac Z.java
    RUN javac HolaMundo.java

    CMD ["java", "HolaMundo"]
    

Construir la imagen: 

    docker build -t alvaro/ejercicio_uno
    
    
Ejecutar el contenedor 

    docker run alvaro/ejercicio_uno
    

Ejecutar el contenedor para que se elimine al term
