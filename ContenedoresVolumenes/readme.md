# Volumenes

## Volúmenes anónimos

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
    





