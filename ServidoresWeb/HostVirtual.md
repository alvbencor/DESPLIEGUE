# Creación Hosts Apache

## Sustitucion de la página por defecto

Sustituimos el index.html de 


    sudo nano /var/www/html/index.html

por el nuestro y podremos ver nuestra página en localhost o con nuestra dureccion (comando *ifconfig*)

    ifconfig





## Servidores Virtuales (por nombre)

Podemos hacer que diferentes páginas web apunten a la misma ip.

Creamos el directorio de nuestra web:

    sudo mkdir /var/www/nombrecarpeta


Y los html:

    sudo nano /var/www/nombrecarpeta/index.html
    

Creamos los archivos de configuracion:

    cd /etc/apache2/sitesavailable
    
    nano /etc/apache2/sites-available/nombrecarpeta.conf


Se recomienda copiar el 00-default.conf












## Por puertos

Mirar los puertos que estan abiertos

  nestat -tuna

Verificamos que el puerto que vayamos a usar que no lo este utilizando nada. 

creamos carpeta:

  sudo mkdir /var/www/porpuerto
  
  nano /var/www/porpuerto/index.html


Creamos el archivo de configuracion

  touch /etc/apache2/sites-available/porpuerto.conf
  

Cambiamos al puerto:

*:8081

**Habilitamos el puerto elegido**

  nano /etc/apache2/ports.conf


++++

  Listen:8081

Desactivamos todo:

  a2dissite *


  a2ensite porpuerto


  apache2 reload
  


  netstat -tuna


## Por direccions IP



