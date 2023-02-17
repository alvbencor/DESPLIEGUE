# Volumenes

Tipos de datos:

- Aplicacion y su entorno de ejecución. Son inmutables una vez generada la imagen.
- Datos , información generada mientras el contenedor esta en ejecucion . Desaparecerán cuando termine la ejecución del contenedor (datos temporales)
- Datos permanentes: ficheros de texto, bbdd... (volumenes)

## Volúmenes anónimos

Para crear un volumen anónimo se incluye en el dockerfile la directiva VOLUME indicando la carpeta **interna del contenedor**

  VOLUME["rutaRelativa"]

Un volumen declarado de esta forma no tendrá nombre y, al desaparecer el contenedor, el 
volumen desaparecerá con él siempre y cuando el contenedor se haya arrancado con la opción 
**--rm**. Si no es así, el volumen quedará “huérfano” y habrá que eliminarlo de propio intento.

#### Docker volume ls

Ver los volúmenes existentes

#### Docker volume prune

Se eliminarán los volúmenes no utilizados

## Volúmenes con nombre

Un volumen de este tipo si permanece tras la eliminación del contenedor, por lo que son 
una buena solución **para los datos que deben persistir**. Aun así, no servirían para almacenar 
datos que necesiten ser editados o accedidos directamente, ya que siguen estando en una 
ubicación desconocida.

Un volumen con nombre no se indica en el fichero Dockerfile sino que se declarará al 
arrancar el contenedor incluyendo la opción -v:

    -v nombreVol:ubicacionInternaDelContenedor
    
    

    docker run -d -v nombre_del_volumen:/ruta/en/el/contenedor nombre_de_la_imagen


Ejemplo 

    docker run -d -v datos:/usr/share/nginx/html nginx
    
Para poder arrancar un contenedor con un volumen con nombre es necesario que el volumen exista previamente.

    docker volume create nombre_del_volumen
    

Si se quiere arrancar otro contenedor con el mismo volumen, bastará con indicar el mismo nombre de voulumen.


## Binding Mounts

Consisten en montar ubicaciones conocidads dentro del host dentro del contenedor. 

Los bind mounts los maneja el usuario, mientras los volumenes los maneja doker

El montaje sobre un directorioi del contenedor que no esta vacio **reemplaza el contenido original del contenedor**

Los cambios ejecutados desde el contenedor sobre los archivos del bind mount **reemplazan por defecto los archivos originales del host**

Es un sistema adecuado para almacenar datos persistentes que deban ser accesibles para el usuario.


Se crean igual que los volumenes pero en lugar de indicar un nombre de volumen se indicara la **ruta absoluta**

    -v dutaExterna:rutaInterna
    

### Combinar y unir volumenes

Para evitar eliminar contenido necesario es posible crear en el arranque del contenedor o dockerfile volumenes anónimos para almacenar el contenido que no se quiera mapear.












