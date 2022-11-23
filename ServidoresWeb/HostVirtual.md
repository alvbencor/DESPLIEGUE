# Creación Hosts Apache

## Sustitucion de la página por defecto

Sustituimos el index.html de 


    cd /var/www/

por el nuestro y podremos ver nuestra página en localhost.


## Hosts Virtuales 



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



