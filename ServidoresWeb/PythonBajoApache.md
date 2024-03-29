# Python bajo Apache

[Instalación del módulo python en apache](#id1)<br>
[Creración de la estructura de la app](#id2)<br>
[Creación del controlador](#id3)<br>
[Configuración de VirtualHost](#id4)<br>

<hr>
<div id='id1' /><br>

## Instalacion de módulo python


En principio, necesitamos hacer que Apache, incorpore un soporte para servir archivos Python. Para ello, necesitaremos habilitarle un módulo, que brinde este soporte.

Existen varios módulos de Apache que brindan soporte para correr archivos Python. Usaremos el módulo mod-wsgi-py3. Para habilitarlo, instalamos el paquete libapache2-mod-wsgi-py3:

~~~
sudo apt-get -y install libapache2-mod-wsgi-py3
~~~
<div id='id2' /><br>

## Creación de la estructura de la aplicación


Después, necesitamos un **directorio destinado a montar toda la aplicacion** y la diviremos en dos partes. Por una parrte tendremos una carpeta destinada a servir la aplicacion publicamente y por otro una carpeta privada (directorio no servido) dedicado al almacenaje de la aplicacion. Añadiremos una tercera carpeta para almacenar los logs de errores y accesos de nuestra app. Los ficheros los creará automáticamente.

~~~
mkdir var/www/miapp

mkdir var/www/miapp/app
mkdir var/www/miapp/public_html
mkdir var/www/miapp/logs
~~~
<div id='id3' /><br>



## Creación de un controlador para la aplcación

Necesitamos un **controlador** para la aplicación, para manejar las peticiones del usuario (las URI a las cuales el usuario accede a través del navegador).

Este archivo controller.py actuará como un pseudo front controller, siendo el encargado de manejar todas las peticiones del usuario, haciendo la llamada a los módulos correspondientes según la URI solicitada.

Dicho módulo, solo se encargará de definir una función, que actúe con cada petición del usuario. Esta función, deberá ser una función WSGI aplicación válida. Esto significa que:

1. Deberá llamarse **application**
2. Deberá recibir dos parámetros: environ, del módulo os, que provee un diccionario de las peticiones HTTP estándar y otras variables de entorno, y la función start_response, de WSGI, encargada de entregar la respuesta HTTP al usuario.
~~~
echo '# -*- coding: utf-8 -*-' > miapp/app/controller.py
~~~

~~~
def application(environ, start_response): 
    # Genero la salida HTML a mostrar al usuario 
    output = "<p>Bienvenido a mi <b>PythonApp</b>!!!</p>" 
    # Inicio una respuesta al navegador 
    start_response('200 OK', [('Content-Type', 'text/html; charset=utf-8')]) 
    # Retorno el contenido HTML 
    return output
~~~
<div id='id4' /><br>

## Configuramos el VirtualHost

En la buena configuración de nuestro VirtualHost, estará la clave para correr nuestra aplicación Python a través de la Web.

Mientras que el DocumentRoot de nuestro sitio Web, será la carpeta pública, public_html, una variable del VirtualHost, será la encargada de redirigir todas las peticiones públicas del usuario, hacia nuestro front controller. Y la variable que se encargue de esto, será el alias WSGIScriptAlias:

~~~
sudo nano /etc/apache2/sites-available/miapp.conf
~~~

Una vez allí, escribimos el contenido del nuevo virtual host:

~~~

<VirtualHost *:80> 
  ServerName python-web

  DocumentRoot /directorio/miAplicacion/public_html 
  WSGIScriptAlias / /directorio/miAplicacion/controller.py 
  ErrorLog /directorio/miAplicacion/logs/errors.log 
  CustomLog /directorio/miAplicacion/logs/access.log combined 

  <Directory /> 
    Options FollowSymLinks 
    AllowOverride All 
  </Directory> 
</VirtualHost>

~~~
Para solucionar el problema de algunos compañeros de clase: introducir en el diretory:

~~~
<Directory /> 
    Options FollowSymLinks 
    AllowOverride none
    Require all granted
  </Directory> 
~~~
Una vez configurado nuestro VirtualHost:

Habilitamos el sitio web: 
~~~
sudo a2ensite miapp
~~~
En caso de que de error, para deshabilitar:
~~~
sudo a2dissite miapp
~~~

Pedirá activar la nueva configuración:
~~~
systemctl reload apache2
~~~

Recargamos Apache: 
~~~
sudo service apache2 reload
~~~
Habilitamos el sitio en nuestro host: 
~~~
sudo nano /etc/hosts y allí agregamos la siguiente línea: 127.0.0.1 miapp
~~~

## Error Internal Server

A la hora de introducir en el navegador http://miapp nos da el siguiente error.

> **Error Internal Server**<br>
The server encountered an internal error or misconfiguration and was unable to complete your request.
Please contact the server administrator at [no address given] to inform them of the time this error occurred, and the actions you performed just before this error.
More information about this error may be available in the server error log.
Apache/2.4.52 (Ubuntu) Server at miapp Port 80

**Al buscar la información en el archivo de logs de apache, aunque no especifica, se debe a la incompatibilidad de la version de python con el módulo instalado.**


> **Nota**<br><br>
Agregar un nuevo hostname a nuestro /etc/hosts nos permitirá seguir trabajando normalmente con nuestro localhost, sin que nuestras aplicaciones Python interfieran con otras, ya sean webs estáticas en HTML o dinámicas en PHP u otro lenguaje.
