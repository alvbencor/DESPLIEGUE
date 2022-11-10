# Ejercicio 11

> Personaliza las páginas de error para el host virtual con el que has estado trabajando 
en el ejercicio 9. Para ello busca dos códigos de errores que no se hayan utilizado en el 
ejemplo (y que puedas reproducir de alguna manera). <br><br>
> Configura certificados TLS para los distintos host virtuales que tengas creados<br><br>


~~~
<VirtualHost *:443>
  ServerAdmin hola@alvarobenito.es
  DocumentRoot /var/www/pagina.es
  ServerName pagina.com
  ServerAlias www.pagina.es
  ErrorLog /var/www/pagina.es/logs/errors.log
  CustomLog /var/www/pagina.es/logs/access.log combined
  
  ErrorDocument 404 /error/error_404.html
  ErrorDocument 500 "Nos hemos ido a la chingada, wey"

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

        SSLEngine On
	      SSLCertificateFile /etc/apache2/certs/apache2.crt
	      SSLCertificateKeyFile /etc/apache2/certs/apache2.key
        SSLProtocol All -SSLv3 
</VirtualHost>
~~~

## Certificado SSL/TLS

### Crear carpeta: 
~~~
alvaro@alvaro:/etc/apache2/certs$ sudo mkdir certs
~~~

### Creamos el certificado con su clave:

~~~
sudo openssl req -x509 -days 365 -newkey rsa:2048 -keyout /etc/apache2/certs/apache2.key -out /etc/apache2/certs/apache2.crt
~~~

Introducimos los campos requeridos del certificado.



### Editamos el .conf de la pagina:

Cambiamos el puerto del virtual host:

~~~
<VirtualHost *:443>
~~~


Añadimos el certificado que hemos creado y la llave. 
~~~
        SSLEngine On
	      SSLCertificateFile /etc/apache2/certs/apache2.crt
	      SSLCertificateKeyFile /etc/apache2/certs/apache2.key
        SSLProtocol All -SSLv3
~~~

Comprobamos en el navegador añadiendo la **s** a http:  **https://www.pagina.es**   y se muestra la pantalla de que el certificado de la página no es de confianza. 






