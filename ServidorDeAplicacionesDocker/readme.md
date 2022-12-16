# Tema 3: Docker

<a name="index">
 
### INDEX<br>
 
 1. [Introducción](#introduccion)<br>
 2. [Imagen](#imagen)<br>
  2.1 [Comandos de imágenes](#comandosImagen)<br>
  2.1 [Equivalencias](#equivalencias)<br>
 3. [Contenedor](#contenedor)<br>
  3.1 [Comandos de contenedores](#comandosContenedor)<br>
 4. [Registro](#registro)<br>
 
 ----
 
## <a name="introduccion">Introduccion</a>

Docker es una plataforma de software que facilita la creación, implementación y ejecución de aplicaciones mediante el uso de contenedores.

Permite crear aplicaciones o servicios que sean independientes y portables, sin importar el sistema operativo o el hardware de cada máquina. Evita tener que instalar dependencias en el host o servidor o hacer uso de máquinas virtuales. 

 
[↑ index](#index) 

## <a name="imagen">Imagen</a>

Es un paquete ejecutable que incluye todo lo necesario para ejecutar un software.

Es una especie de representación estática de una aplicación o servicio, de su configuración y todas sus diferencias. 

Una imagen podría contener un sistema operativo ubuntu con un servidor apache y una aplicación web instalada. Normalmente al crear imágenes se parte de una imagen padre a la que se le van añadiendo cosas. 

Para ejecutar la aplicación o servicio, se crea una instancia de esa imagen, el contenedor, que se ejecutará en el host de Docker. Las imágenes, al ser plantillas, van a ser usadas para crear nuevos contenedores y nunca cambian a no ser que se cree una nueva a partir de un contenedor. 

En resumen, los contenedores son instancias en ejecución de una imagen y son los que realmente ponen en marcha las aplicaciones y servicios de esa imagen. A partir de una misma imagen, es posible ejecutar diferentes contenedores. 
 
 ### <a name="comandosImagen">Comandos de imagen</a>

| Comando | Descripción |
| --- | --- |
| docker image ls | Listar imágenes |
| docker search *item* | busca nombres de imágenes que tengan un nombre relacionado con *item*|
| docker image history *nombreImagen* | ver el historial de una imagen, como se construyó |
| docker image prune | Borra las imagenes que no se esten utilizando siempre que no haya ningún contenedor de la misma. |
| docker image prune -a | Borra todas las imágenes no utilizadas |
| docker image rm *nombreImagen* | Borra una (o más imágenes) |
| docker image rm -f *nombreImagen* | Si existen contenedores de la imagen, para borrarla hay que forzarlo con la opción **-f** |
| docker image pull *nombreImagen* | Descargar imágenes de un repositorio. Por defecto, la versión más actual |
| docker image pull *nombreImagen*:*nombreEtiqueta* | Descarga una etiqueta en concreto |
| docker image push *nombreImagen* | Subir imágenes a un registro (es necesario estar dado de alta y logeado primero : p.e. DockerHub) |
| docker image push *nombreImagen:nombreEtiqueta* | Subir una etiqueta de una imagen a un registro |
| docker image inspect | Se ve informacion detallada de una o más imagenes (etiquetas, comandos, versiones...) |
| docker image build *nombreImagen* path | Permite crear imágenes propias a traves del **DockerFile**. |
| docker image build *nombreImagen:nombreEtiqueta* | Igual que el anterior |


[↑ index](#index)
 
###  <a name="equivalencias">Equivalencias</a>

- **docker images** tiene el mismo resultado que **docker image ls**

- **docker rmi imagen** es la versión corta de **docker image rm imagen**

- **docker pull imagen** hace lo mismo que **docker image pull imagen**

- **docker push imagen** es equivalente a **docker image push imagen**

 
 
[↑ index](#index)
 
 
## <a name="contenedor">Contenedor</a>

Instancia en ejecución de una imagen.

Es un paquete de código completado con las dependencias y herramientas necesarias para poder ejecutar dicho código (librerías del sistema, entorno de ejecución, cualquier tipo de configuracion ...) describiendolo en un archivo de configuracion llamado **DockerFile**.

La **ventaja** del uso de contenedores es que pueden ser versionados, reutilizados y replicados fácilmente por administradores de sistemas u otros codificadores sin necesidad de conocer el funcionamiento interno de la aplicación. 
 
### <a name="comandosContenedor">Comandos de contenedores</a>

| Comando | Descripción |
| --- | --- |
| docker run *nombreImagen* | Ejecutar un contenedor |
| docker run --name *nombreContenedor nombreImagen* | Se le puede dar un nombre concreto al contenedor con el comando **--name** pero no puede estar asignado a otro contenedor.|
| docker run -d *nombreImagen | Ejecuta un contenedor en segundo plano |
| docker run -it *nombreImagen* /bin/bash | permite ejecutar la consola del contenedor para poder trabajar con ella (-it : terminal interactivo). Para salir de la consola del contenedor: **Ctrl+p Ctrl+q**|
| docker ps -a | Listar todos los contenedores en funcionamiento (**ps**) y si se quiere ver todos los que están parados **-a** |
| docker ps --format *nombresCampos* | Listar contenedores indicando las columnas que se quieren mostrar en el listado. *nombresCampos* tendrá el siguiente formato: “table {{ .NombreCol1 }}\t{{.NombreCol2}}\t{{ .NombreColN }}” |
| docker stop *ID/nombreContenedor* | Parar un contenedor en ejecución |
| docker stop $(docker ps -a -q) | Parar todos los contenedores |
| docker kill *ID/nombreContenedor* | forzar la parada con **kill** |
| docker start *ID/nombreContenedor* | Volver a arrancar un contenedor parado con anterioridad |
| docker rm *ID/nombreContenedor* | Para eliminar un contenedor |
| docker rm $(docker ps -a -q) | Elimina todos los contenedores después de pararlos todos con *docker stop $(docker ps -a -q)* |
| docker build -t vieux/apache:2.0 . | Etiquetar una imagen (**-t , --tag**) |


[↑ index](#index)
 
 
## <a name="registro">Registro</a>

Aplicación para gestionar almacenamiento y envío de imágenes de contenedores. Pueden ser públicos o privados (DockerHub, Amazon Web Services, Aure, Google...)

