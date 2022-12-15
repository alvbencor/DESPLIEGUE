## Ejercicio2

Este ejercicio va a servir para ir familiarizándote con Docker.
- Primero vas a probar todos los comandos vistos hasta el momento, salvo push y build. Para ello, descarga la imagen codenvy/javascript_html.

| Descripcion | Comando |
| --- | --- |
| Listar imágenes | <code>docker image ls </code>|
| Buscar imágenes | <code>docker search *buscar* </code>|
| Historial imágenes | <code>docker image history *nombreImagen* </code>|
| Eliminar imágenes en deshuso | <code>docker image prune -a </code>|
| Borrar imágenes | <code>docker image rm *nombreImagen* </code>|
| Forzar borrado de imágenes | <code>docker image rm -f *nombreImagen* </code>|
| Descargar imágenes | <code>docker image pull *nombreImagen* </code> |
| Descargar version de imagen imágenes | <code>docker image pull *nombreImagen*:*nombreEtiqueta* </code>|
| Subir imagen | <code>docker image push *nombreImagen* </code>|
| Subir imagen con nombre etiqueta  | <code>docker image push *nombreImagen:nombreEtiqueta* </code>|
| Subir imagen | <code>docker image bulid *nombreImagen* path </code>| 

....








- Ve a Docker Hub y date de alta: https://hub.docker.com/**alvbencor**
- Busca imágenes que contenga html, java, php(por separado). Verás que hay
imágenes de dos tipos:
     - nombre: Las que solo tienen un nombre son imágenes oficiales y las que se
recomienda usar:

     - nombre/otroTexto: Las que tienen este formato son imágenes creadas por una persona o empresa:


