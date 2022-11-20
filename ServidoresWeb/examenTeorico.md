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

Esta página está referenciada en 

    cd /etc/apache2/sites-available/000-default.conf
    

### Configuracion del servidor

ir a la carpeta de archivos de configuracion:

    sudo /ect/apache2

El hecho de que la configuración esté repartida en diferentes ficheroshace más facil su mantenimiento y resulta más modular a la hora de activar o desactivar según que caraterísticas:

#### apache2.conf

Es el fichero principal de apache, donde se pueden realizar cambios generales.

    cat /etc/apache2/apache2.conf
    


Para establecer el **modelo de seguridad** que se aplicará por defecto:

    <Directory/>
        Options Indexes FollowSymlinks
        AllowOverride None
        Require all granted
      </Directory>
 
**AccessFieName .htaccess**: el valor será el nombre del fichero que hay que buscar en cada directorio para directivas adicionales de configuración

**Include ports.conf**: Incluye la lista de puertos a traves de los que escuchar. Referencia al fichero ports.conf.

Otras directivas interesantes que modifican esta configuración son: 

| Directiva | Descripción | Ejemplo de uso |
| --- | --- | --- |
| **ServerName** | Nombre de equipo y puerto que usa el servidor para identificarse ante los clientes. **Indica el nombre del sitio web** | ServerName www.pagina.es:80 |
| **ServerRoot** | Indica la carpeta en la que se ha instalado el servidor. **No es la carpeta de archivos de configuración** | ServerRoot /usr/local/apache |
| **ServerAdmin** | Direccion de correo del administrador del servidor web. En caso de error se mostrará al usuario para que reporte culaquier incidencia. | ServerAdmin hola@alvarobenito.es |
| **Listen** | Especifica los puertos del servidor en los que escucha a los clientes y, opcionalmente las IPs de los adaptadores de la red que utiliza. | Listen 80 Listen 192.168.3.5:8080 |
| **TimeOut** | Máximo tiempo en segundos que el servidor expera un nuevo mensaje de un cliente para no cerrar la conexion | TimeOut 300 |
| **KeepAlive** | Para indicar que se mantenga (on) o no (off) una conexion con un cliente para vaias transacciones | KeepAlive on / KeepAlive off |
| **DocumentRoot** | Define la ruta del equipo donde estan todos los ficheros que se sirven en cada momento a traves del sitio web. Todo lo que haya en este directorio está en principio suendo ofrecido a traves de la web | DpcumentRoot var/web |
| **DirectoryIndex** | Indica los nombres de las páginas web índice que puede entrefar el servidor por defecto cuando en la peticion http la URL contiene un solo nombre de carpeta | DirectoryIndex index.html home.html index.php |
| **NameVirtualHost** | Especifica las direcciones IP y puerto en los que el servidor recibirá peticiones para sitios web virtuales basados en nombre. Sise usa esta directiva, se deben definir los sitios virtuales dentro de una directiva. <VirtualHost>...</VirtualHost> | NameVirtualHost*:8 |
| **ErrorLog** | Fichero donde se registran los errores que se produzcan | /var/log/error_log |
    
#### envars
Contiene la configuración de las variables de entorno

#### ports.conf

    cat /etc/apache2/ports.conf
    
Archivo de configuracion en el que se establecen los puertos en los que escucha Apache. Es un fichero que no se suele modificar porque los puertos escucha suelen ser estandar, pero **uno de los casos en los que si se cambia es para configurar el soporte para HTTPS**.

De inicio, Apache escucha en el puerto 80. El modulo ssl escucha en el 443 y gnutls tambien en el 443.


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

Aquí se localiza el fichero **000-default.conf** que contendrá la configuracion del servidor virtual por defecto. Un enlace a este fichero se encontrá en **sites-enabled**.

#### sites-enabled
Contiene enlaces simbólicos a los ficheros de configuracion cuyos hosts virtuales se encuentran activos en este momento. 

### *Logs* del servidor

Los ficheros de log se encuentran en 

    cd /var/log/apache2
    

#### access.log
Por defecto, almacenará informacion de cada petición que llegue al servidor

#### error.log
Por defecto, en se almacena información de los errores que se produzcan


## Configuración de Apache

### apache2.conf



### ports.conf


















  

  
