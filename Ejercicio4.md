# Trabajar con Docker

Crear una imagen:
- a partir de un contenedor haciendo las modificaciones necesarias
- crear el dockerfile


## Imagen para una página estática

Ejecutar la imagen de apache

    docker run -d --name apache2 -p 82:80 bitnami/apache
    
## Ejercicio 4

¿Que hace la opcion -p?
 -p Publish a container's port(s) to the host
 
 ¿Qué opción debería usarse si se quiere que Docker asigne de forma aleatoria un
puerto del host al puerto asignado a Apache en el contenedor?

-P

