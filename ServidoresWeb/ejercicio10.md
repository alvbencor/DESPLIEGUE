# Ejercicio 10

Autenticación HTTP<br>
[Autenticación con .htaccess](#htaccess)

>  Para algún host virtual de los que tengas creados, asigna autenticación (de alguna de
las formas que se ha visto) a dos carpetas diferentes del directorio (si no tienes crea
alguna) y da permisos de acceso a sendos usuarios.

## Creamos usuarios

Instalamos el paquete **apache2 utils** si no lo está
~~~
sudo apt-get update
sudo apt-get install apache2 utils
~~~

Usamos el comando **htpasswd** para crear el fichero con la opcion **-c**

Si se utiliza esta opción sobre un fichero creado **se sobreescribiría**

~~~
htpasswd -c /etc/apache2/.htpasswd alvaro
htpasswd /etc/apache2/.htpasswd fati
~~~

Pedirá introducir y confirmar contraseña.

~~~
sudo nano /etc/apache2/envvars
~~~

## Asignamos permisos

~~~
# Since there is no sane way to get the parsed apache2 config in scripts, some
# settings are defined via environment variables and then used in apache2ctl,
# /etc/init.d/apache2, /etc/logrotate.d/apache2, etc.
export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data
# temporary state file location. This might be changed to /run in Wheezy+1
export APACHE_PID_FILE=/var/run/apache2$SUFFIX/apache2.pid
export APACHE_RUN_DIR=/var/run/apache2$SUFFIX
export APACHE_LOCK_DIR=/var/lock/apache2$SUFFIX
# Only /var/log/apache2 is handled by /etc/logrotate.d/apache2.
export APACHE_LOG_DIR=/var/log/apache2$SUFFIX

~~~

Asignamos:
~~~
sudo chown www-data:www-data /etc/apache2/.htpasswd
~~~

En las páginas que queramos asignar permisos tenemos que incluir en 
~~~
sudo nano /etc/apache2/sites-available/pagina.es.conf
~~~
las directivas:
- AuthType Basic
- AuthName
- AuthUserFile
- Require (usuario válido)
- 

>  Como en el momento de hacer este ejercicio no tenía ninguna web en el servidor de apache, cree www.pagina.es<br>
Ver proceso [**aquí**]()
>
~~~

<VirtualHost *:80>
  ServerAdmin hola@alvarobenito.es
  DocumentRoot /var/www/pagina.es
  ServerName pagina.com
  ServerAlias www.pagina.es
  ErrorLog /var/www/pagina.es/logs/errors.log
  CustomLog /var/www/pagina.es/logs/access.log combined

        <Directory "/var/www/pagina.es/">
                AuthType Basic
                AuthName "Acceso Restringido a usuarios"
                AuthUserFile /etc/apache2/.htpasswd
                Require user fati
        </Directory>

        <Directory "/var/www/pagina.es/private/">
                AuthType Basic
                AuthName "Acceso Restringido a usuarios"
                AuthUserFile /etc/apache2/.htpasswd
                Require user alvaro
        </Directory>
</VirtualHost>
st>
~~~

Recargamos apache y debería de funcionar si las rutas y permisos son correctos:
 
~~~
sudo service apache2 restart
~~~

<div id="htaccess"></div>

# Autenticación con .htaccess

Modificamos el fichero de configuración de Apache
~~~
sudo nano /etc/apache2/apache2.conf
~~~
Y cambiamos en el directorio /var/www/ AllowOverride **All**, permitiendo que la política sobre
dicho directorio sea diferente si así se define con algún fichero .htaccess

~~~
<Directory />
        Options FollowSymLinks
        AllowOverride None
        Require all denied
</Directory>

<Directory /usr/share>
        AllowOverride None
        Require all granted
</Directory>

<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>
~~~
Y, ya en el directorio que se quiere proteger, se incluye un fichero .htaccess con el
siguiente contenido:

~~~
AuthType Basic
AuthName "Acceso restringido a monguers"
AuthUserFile /etc/apache2/.htpasswd
Require user fati
~~~

En este caso, el usuario que puede acceder es *fati*





