# 4. Contenedores

#### <a name="INDEX">INDEX</a>


[Ejecutar contenedor](#Ejecutar)<br>
[Listar contenedores](#Listar)<br>
[Manejar contenedores](#Manejar)<br>
[Ejecutar comandos Linux en un contenedor](#EjecutarLinux)<br>
[Guardar contenedor como imagen](#Guardar)<br>

[Ejercicio 3](#Ejercicio3)

> ### IMPORTANTE ejecutar comandos con sudo su


## <a name="Ejecutar">Ejecutar contenedor</a>

    sudo docker run nombreimagen
  
Es posible darle un nombre concreto al contenedor, mediante la opción --name. El nombre
no puede estar asignado ya a otro contenedor:

    docker run --name nombreContenedor nombreImage

Otra de las opciones interesantes es ejecutar el contenedor en segundo plano para poder
seguir trabajando con la consola de docker. Esto se consigue con la opción -d:

    docker run -d nombreImagen
    
Docker también permite ejecutar la consola del contenedor para poder trabajar con ella (la
opción -it permite tener un terminal interactivo):

    docker run -it nombreImagen /bin/bash
    
Para poder salir de la consola del contenedor: Ctrl+p Ctrl+q

#### [↑  INDEX](#INDEX)

## <a name="Listar">Listar contenedor</a>

Para listar todos los contenedores en funcionamiento, se utiliza el comando ps. Si se
quieren ver también los que están parados, se utilizará la opción -a:

    docker ps -a
    
Otra opción disponible para listar contenedores es indicar las columnas que se quieran
mostrar en el listado. Se indicará con la opción –format seguida de los nombres de los campos
que se quieren mostrar:

    docker ps --format nombresCampos
    
nombresCampos tendrá el siguiente formato(\t es el separador, podrá ser cualquiera):

    “table {{ .NombreCol1 }}\t{{.NombreCol2}}\t{{ .NombreColN }}”
    
En el siguiente enlace se pueden ver los nombres de cada columna de la tabla:
https://docs.docker.com/engine/reference/commandline/ps/


#### [↑  INDEX](#INDEX)

## <a name="Manejar">Manejar contenedor</a>

Para parar un contenedor en ejecución se hace uso del comando stop y es necesario
indicar el ID o el nombre del contendor:

    docker stop IDoNombreContendor

Y para parar todos los contenedores:

    docker stop $(docker ps -a -q)

Si no se puede parar el contenedor con stop, se puede forzar la parada con el comando kill:

    docker kill IDoNombreContendor
    

Si se quiere volver a arrancar un contenedor parado con anterioridad, se usa el id o el
nombre con el comando start:

    docker start IDoNombreContendor
    
Como ya se ha visto, cuando se para un contenedor no se elimina y es posible volverlo a
arrancar. Para eliminarlo definitivamente se usa el comando rm seguido del ID o el nombre del
contendor:

    docker rm IDoNombreContendor
    
Y si lo que se quiere es eliminar todos los contenedores, tras pararlos con la opción vista
con anterioridad, se puede hacer:

    docker rm $(docker ps -a -q)
    

#### [↑  INDEX](#INDEX)

### <a name="EjecutarLinux">Ejecutar comandos Linux en un contenedor</a>

En puntos anteriores se ha visto que se podía arrancar el contenedor entrando a la vez en
la consola del mismo. En caso de que el contenedor ya esté corriendo, hay dos alternativas:

Por un lado, se puede ejecutar directamente un comando en el contenedor:

    docker exec IDoNombreContendor comando
    
Como segunda opción, se puede abrir el terminal del contenedor:

    docker exec -it nombreContenedor /bin/bash
    

#### [↑  INDEX](#INDEX)

### <a name="Guardar">Guardar contenedor como imagen</a>

Ya se ha dicho que los cambios realizados en un contenedor se pierden a no ser que se
haga una nueva imagen a partir del mismo. Tras detener el contenedor al que se le han
aplicado ciertos cambios, se puede crear una imagen mediante el comando commit:

    docker commit IDoNombreContenedor nombreImagen:nombreTag
    


#### [↑  INDEX](#INDEX)

# <a name="Ejercicio3">Ejercicio 3</a>

- Lista los contenedores que tienes (corriendo y parados).
- Elimina todos los contenedores.
- Arranca, en segundo plano, la imagen que descargaste para el ejercicio 2 con el
nombre codEnvJsHtml.
- Una vez arrancada lista el contenido de su directorio raíz.
- Para el contenedor.
- Arranca la imagen, de nuevo con el nombre codEnvJsHtml. ¿Qué pasa? Si hay
algún problema, soluciónalo siguiendo las indicaciones que te haya dado docker.
- Reinicia el primer contendor.
- Lista los contenedores. ¿Cuántos hay?
    
