# Ejercicio 9

> Red Hat Enterprise Linux 3: Manual de referencia
Anterior	Capítulo 10. Servidor Apache HTTP<br> 
http://web.mit.edu/rhel-doc/3/rhel-rg-es-3/s1-apache-config.html

*Dentro de mods-available, visualiza algún fichero .load y observa cómo se utiliza la
directiva LoadModule para cargar el módulo en cuestión. Busca cual es la
funcionalidad de LoadModule.

## LoadModule
LoadModule es usada para cargar en módulos Dynamic Shared Object (DSO). Son librerías que son cargadas dinamicamente en tiempo de ejecución.

Ya no es importante el orden en que se cargan estos módulos con el Servidor Apache HTTP 2.0. 


*Edita, después, algún fichero .conf(por ejempl dir.conf) y observa cómo se añaden
directivas dentro de una declaración IfModule. Busca cual es la funcionalidad de
IfModule y, también, que indica la directiva DirectoryIndex.

## IfModule
Las etiquetas <IfModule> y </IfModule> crean un contenedor condicional que sólo es activado si el módulo especificado es cargado. Las directivas contenidas entre etiquetas IfModule son procesadas bajo una de dos condiciones. Las directivas son procesadas si se carga el módulo entre la etiqueta de comienzo <IfModule>. O, si un símbolo de exclamación [!] aparece antes del nombre del módulo, entonces las directivas son procesadas sólo si el módulo especificado en la etiqueta <IfModule> no es cargado.

## DirectoryIndex
  
DirectoryIndex es la página por defecto que entrega el servidor cuando hay una petición de índice de un directorio especificado con una barra (/) al final del nombre del directorio.

Cuando un usuario pide la página http://ejemplo/este_directorio/, recibe la página del índice del directorio, DirectoryIndex, si existe, o un listado de directorios generado por el servidor. El valor por defecto para DirectoryIndex es index.html y el tipo de mapa index.html.var. El servidor intentará encontrar cualquiera de estos archivos y entregará el primero que encuentre. Si no encuentra ninguno de estos archivos y Options Indexes esta configurado para ese directorio, el servidor genera y devuelve una lista, en formato HTML, de los subdirectorios y archivos dentro del directorio, a menos que la característica de listar directorios esté desactivada.


*Habilita (y si no está disponible instala antes) el módulo **userdir**. Verifica que se ha
habilitado. Busca para que sirve ese módulo y alguna forma de probarlo*
  
  ## UserDir
  
UserDir es el nombre del subdirectorio dentro del directorio principal de cada usuario dónde estarán los archivos HTML personal que serán servidos por el servidor de Web. Esta directiva esta configurada por defecto a disable.

El nombre para el subdirectorio esta configurado a public_html en la configuración por defecto. Por ejemplo, el servidor puede recibir la siguiente petición:
  
  > http://example.com/~username/foo.html
  
  El servidor buscará por el archivo:
  
  > /home/username/public_html/foo.html
  
  En el ejemplo de arriba, /home/username/ es el directorio principal del usuario (observe que la ruta por defecto al directorio principal del usuario puede variar).

Hay que asegurarse que los permisos de los directorios principales de usuario esten configurados correctamente. El valor de los permisos deben ser de 0711. Los bits de lectura (r) y ejecución (x) deben estar activados en el directorio del usuario public_html (0755 también funcionará). Los archivos servidos en un directorio principal de usuario public_html debe estar configurados, por lo menos, a 0644.


  
  
