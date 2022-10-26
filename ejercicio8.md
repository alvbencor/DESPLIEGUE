- ¿Cuál es el módulo que se instala y activa para poder desplegar aplicaciones
desarrolladas con Python?

~~~
sudo apt-get -y install libapache2-mod-wsgi-py3
~~~

- ¿Dónde se almacena el fichero de configuración del host virtual?

~~~
sudo nano /etc/apache2/sites-available/webPython
~~~

> Falta el .conf

- ¿Cuál es el directorio raíz de la aplicación a desplegar?
~~~
Documents/webApp
~~~

- ¿Dónde se almacenarán los logs generados por la aplicación?
