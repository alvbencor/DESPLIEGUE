# Apache Server

Apache HTTP Server (httpd) es un software de servidor web de código abierto y gratuito, que garantiza el rendimiento, estabilidad y seguridad de un servidor web, mantenido y desarrollado por la apache software foundation y disponible para Windows, y GNU/Linux entre otros. 

Http es el programa servidor del protocolo Apache HTTP. Está diseñado para ser ejecutado como un proceso autónomo, no interactivo y en segundo plano(daemon)

## Características de apache

Es un servidor web con soporte para http/1.1 y http/2.0

### Arquitectura

- Está cifrado en **módulos**
- Cada módulo contiene un conjunto de funciones relativas a un aspecto concreto del servidor. 
- La funcionalidad de estos módulos puede ser activada o desactivada al arrancar el servidor. 
- Los módulos de Apache se pueden clasificar en tres categorías:
    - **Módulos base**: se encargan de las funciones básicas
    - **Módulos multiproceso**: Encargados de la unión de los puertos de la máquina, aceptando las peticiones y atendiéndolas. 
    - **Módulos adicionales**: para añadir funcionalidad al servidor.

Esta estructura basada en módulos permite habilitar o deshabilitar distintas funcionalidades como:
- **Módulos de seguridad** como *mod_security*
- **Módulos** de caché como *Varnish*
- **Módulos** de personalización de cabeceras como *mod_headers*.

Este software incluye entre otros:
- envío mensajes de error personalizados
- esquemas de autenticacion
- modulo de host virtual que permite ejecutar múltiples sitios simultaneamente
- Servicio de nombres de dominio dns
- smtp
- ftp

## Instalación de Apache

    sudo apt install apache2 apache2-utils

### Status, arrancar, parar y recargar Apache

#### Estado del servidor
    sudo systemctl status apache2

#### Arrancar el servidor
    sudo systemctl start apache2

#### Parar el servidor 
    sudo systemctl stop apache2

#### Recargar la configuración
    sudo systemctl reload apache2
    
#### Deshabilitar/habilitar el inicio automático

Apache está configurado por defecto para activarse cuando arranca el sistema operativo. Para odificar esto:

    sudo systemctl disable apache2

Y para habilitarlo de nuevo: 

    sudo systemctl enable apache2

#### Versión instalada
    apache2 -v
    

## Directorios importantes

### Contenido

Ir a la carpeta raiz:
    cd /var/www/html

Aquí es donde se encuentra la página de bienvenida de apache (index.html) que puede ser configurada como una pagina estática.

### Configuracion del servidor

ir a la carpeta de archivos de configuracion:

    sudo /ect/apache2

El hecho de que la configuración esté repartida en diferentes ficheroshace más facil su mantenimiento y resulta más modular a la hora de activar o desactivar según que caraterísticas:

#### apache2.conf

Es el fichero principal de apache, donde se pueden realizar cambios generales.

    cat /etc/apache2/apache2.conf
    
#### envars
Contiene la configuración de las variables de entorno

#### ports.conf
Contiene la configuracion de los puertos donde apache escucha
    cat /etc/apache2/ports.conf

#### conf-available
Contiene ficheros de configuracion adicionales para diferentes aspectos de Apache o de aplicaciones web como *phpMyAdmin*
    cd /etc/apache2/conf-available

#### conf-enabled
Contiene una serie de elaces simbólicos a los ficheros de configuracion adicionales para activarlos. Puede activarse o desactivarse con los comandos **a2enconf** o **a2disconf**

    cd /etc/apache2/conf-enabled

#### mods-available
Contiene los módulos disponibles para usar con apache

#### mods-enabled
Contiene enlaces simbólicos a aquellos módulos de Apache que se encuentran activados en este momento.

#### sites-available
Contiene los ficheros de configuracion de cada uno de los host virtuales configurados y disponibles (activos o no) Se crean utilizando los comandos pertinentes.

# sites-enabled
Contiene enlaces simbólicos a los ficheros de configuracion cuyos hosts virtuales se encuentran activos en este momento. 

### ***Logs* del servidor















  

  
