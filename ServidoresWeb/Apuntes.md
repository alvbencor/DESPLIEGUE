# Apache Server

### <a name="index">INDEX</a>

1. [Características de Apache](#caractApache)
2. [Arquitectura     ](#arq)
3. [Instalación de Apache](#inst)
4. [Manejar el estado del servicio](#estado)
5. [Directorios importantes](#impordir)
6. [Autenticacion http](#authttp)
7. [Autenticacion con htaccess](#htaccess)
8. [Peronalizar las páginas de error](#error)
9. [Configurar SSL/TSL en Apache](#error)

- - - 

[# Directivas importantes](#directivas)     [# Otras directivas](#otrasdirectivas) [# apache2.conf](#apache2.conf)   [# ports.conf](#ports.conf)  [# UserDir](#UserDir) [# DirectoryIndex](#DirectoryIndex)  

---



Apache HTTP Server (httpd) es un software de servidor web de código abierto y gratuito, que garantiza el rendimiento, estabilidad y seguridad de un servidor web, mantenido y desarrollado por la apache software foundation y disponible para Windows, y GNU/Linux entre otros. 

Http es el programa servidor del protocolo Apache HTTP. Está diseñado para ser ejecutado como un proceso autónomo, no interactivo y en segundo plano(daemon)

## <a name="caractApache">Características de Apache</a>

Es un servidor web con soporte para http/1.1 y http/2.0


[↑ INDEX](#index)<br>

## <a name="arq">Arquitectura</a>

- Está cifrado en **módulos**
- Cada módulo contiene un conjunto de funciones relativas a un aspecto concreto del servidor. 
- La funcionalidad de estos módulos puede ser activada o desactivada al arrancar el servidor. 
- Los módulos de Apache se pueden clasificar en tres categorías:
    - **Módulos base**: se encargan de las funciones básicas
    - **Módulos multiproceso**: Encargados de la unión de los puertos de la máquina, aceptando las peticiones y atendiéndolas. 
    - **Módulos adicionales**: para añadir funcionalidad al servidor.

Esta estructura basada en módulos permite habilitar o deshabilitar distintas funcionalidades como:
- **Módulos de seguridad** como *mod_security*
- **Módulos de caché** como *Varnish*
- **Módulos de personalización de cabeceras** como *mod_headers*.

Este software incluye entre otros:
- envío mensajes de error personalizados
- esquemas de autenticacion
- modulo de host virtual que permite ejecutar múltiples sitios simultaneamente
- Servicio de nombres de dominio dns
- smtp
- ftp


[↑ INDEX](#index)<br>

## <a name="inst">Instalación de Apache</a>

    sudo apt install apache2 apache2-utils
    
## <a name="estado">Manejar el estado del servicio</a>

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

Apache está configurado por defecto para activarse cuando arranca el sistema operativo. Para modificar esto:

    sudo systemctl disable apache2

Y para habilitarlo de nuevo: 

    sudo systemctl enable apache2

#### Versión instalada
    apache2 -v
    

[↑ INDEX](#index)<br>


## <a name="impordir">Directorios importantes</a>

### Contenido

Ir a la carpeta raiz:
    
    cd /var/www/html

Aquí es donde se encuentra la página de bienvenida de apache (index.html) que puede ser configurada como una pagina estática.

Esta página está referenciada en 

    cd /etc/apache2/sites-available/000-default.conf
    

[↑ INDEX](#index)<br>

### Configuracion del servidor

ir a la carpeta de archivos de configuracion:

    sudo /ect/apache2

El hecho de que la configuración esté repartida en diferentes ficheroshace más facil su mantenimiento y resulta más modular a la hora de activar o desactivar según que caraterísticas:


[↑ INDEX](#index)<br>

#### <a name="apache2.conf">apache2.conf</a>

Es el fichero principal de apache, donde se pueden realizar cambios generales.

    cat /etc/apache2/apache2.conf
    


Para establecer el **modelo de seguridad** que se aplicará por defecto:

    <Directory/>
        Options Indexes FollowSymlinks
        AllowOverride None
        Require all granted
      </Directory>
 
**AccessFileName .htaccess**: el valor será el nombre del fichero que hay que buscar en cada directorio para directivas adicionales de configuración

**Include ports.conf**: Incluye la lista de puertos a traves de los que escuchar. Referencia al fichero ports.conf.

Algunas <a name="directivas">**directivas** </a>interesantes que modifican esta configuración son: 



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
| **LoadModule** | LoadModule es usada para cargar en módulos Dynamic Shared Object (DSO). Linkea en el archivo o libreria y lo añada a la lista de modulos activos. | --- |
| **UserDir** | La directiva UserDir especifica un directorio del que cargar contenido por usuario. | --- |
| **ifModule** | Las etiquetas <ifmodule> </ifmodule> **crean un contenedor condicional** que solo es activado si el módulo especificado es cargado. Las directivas contenidas entre estas etiquetas son procesadas bajo una de dos condicio | --- |


>  #### <a name="UserDir">UserDir</a>
>En sistemas con multiples usuarios, cada usuario puede tener un sitio web en su directorio home usando la directiva UserDir. Los visitantes de una URL http://ejemplo.com/~username/ recibniran el contenido del directorio home del usuario username en el subdirectorio especificado por la directiva *userdir*.
>Por defecto, el acceso a estos directorios no está activado. Se puede permitir el acceso cuando usa *userdir* quitando el comentario de la linea 
>#Include conf/extra/httpd-userdir


> #### <a name="DirectoryIndex">DirectoryIndex</a>
> DirectoryIndex es la pagina por defecto que entrega el servidor cuando hay una peticion de índice de un directorio especificado con una barra (/) al final del nombre del directorio.
> Cuando un usuario pide la página http://ejemplo/estedirectorio/ , recibe la página del índice del directorio DirectoryIndex si existe, o un listado de directorios generado por el servidor. El valor por defeco para DirectoryIndex es index.html. El servidor intentará encontrar cualquiera de estos archivos y entregara el primero que encuentre. si no encuentra ninguno y Option Indexes esta configurado para ese directorio, el servidor genera y devuelve una lista en html de los subdirectorios y archivos dendtro del directorio, a menos que la caracteristica de listar directorios este desactivada. 

[↑ INDEX](#index)<br>


## <a name="otrasdirectivas">Otras Directivas</a>


#### 

 


#### x






#### 

nes. 


    
#### envars
Contiene la configuración de las variables de entorno

#### <a name="ports.conf">ports.conf</a>

    cat /etc/apache2/ports.conf
    
Archivo de configuracion en el que se establecen los puertos en los que escucha Apache. Es un fichero que no se suele modificar porque los puertos escucha suelen ser estandar, pero **uno de los casos en los que si se cambia es para configurar el soporte para HTTPS**.

De inicio, Apache escucha en el puerto 80. El modulo ssl escucha en el 443 y gnutls tambien en el 443.


#### conf-available
Contiene ficheros de configuracion adicionales para diferentes aspectos de Apache o de aplicaciones web como *phpMyAdmin*
    
    cd /etc/apache2/conf-available

#### conf-enabled
Contiene una serie de elaces simbólicos a los ficheros de configuración adicionales para activarlos. Puede activarse o desactivarse con los comandos **a2enconf** o **a2disconf**

    cd /etc/apache2/conf-enabled

#### mods-available
Contiene los módulos disponibles para usar con apache

#### mods-enabled
Contiene enlaces simbólicos a aquellos módulos de Apache que se encuentran activados en este momento.

#### sites-available
Contiene los ficheros de configuracion de cada uno de los host virtuales configurados y disponibles (activos o no) Se crean utilizando los comandos pertinentes.

Aquí se localiza el fichero **000-default.conf** que contendrá la configuracion del servidor virtual por defecto. Un enlace a este fichero se encontrá en **sites-enabled**.

#### sites-enabled
Contiene enlaces simbólicos a los ficheros de configuración cuyos hosts virtuales se encuentran activos en este momento. 


[↑ INDEX](#index)<br> 


### *Logs* del servidor

Los ficheros de log se encuentran en 

    cd /var/log/apache2
    

#### access.log
Por defecto, almacenará informacion de cada petición que llegue al servidor

#### error.log
Por defecto, en el se almacena información de los errores que se produzcan


[↑ INDEX](#index)<br>

## <a name="authttp">Autenticación http</a>


Permite proteger carpetas personales dentro del servidor web, en este caso apache. Para hacer uso de ella, lo primero es instalar, si no lo está, el paquete **apache2-utils**.

Una de las utilidades que ofrece es manipular archivos de autenticación(con el comando **htpasswd**) que serán los ficheros a traves de los cuales se configurará el acceso, mendiante usuario y contraseña, a esas carpetas protegidas dentro del servidor web.

El comando *htpasswd* mencionado antes, se utiliza tanto para crear el fichero por primera vez y añadir un usuario a la zona protegida que se va a crear, como para añadir otros usuarios una vez creado.

La primera vez, **hay que usar la opcion -c**. Para añadir mas usuarios ya no hay que utilizarla. Si se utilizara, **sobreescribiria el fichero** y se perderían los datos anteriormente almacenados. 

Una vez configurado el usuario y contraseña, hay que asignar esa propiedad al usuario y grupo de apache. En el fichero de variable de entornos de apache ( /etc/apache2/envars).

El siguiente paso es proteger el/los directorios del sitio web. Para esto se incluye la directiva Directory en el fichero de configuracion del sitio web.

Las directivas que se incluyen son:
- **AuthTypeBasic** que define el tipo de autenticacion
- **AuthName** que dfine el mensaje que se mostrara al usuario cuando se le solicite el usuario y contraseña para acceder
- **AuthUserFile**: se indica la ruta al fichero que se ha creado con los usuarios/contraseña que tienen permitido el acceso.
- **Require valid-User**: indica que sólo se podrá acceder con un usuario válido. Si de los usuarios que haya configurados se pretende que sólo tenga permisos de acceso uno de ellos, se puede indicar como sigue: **Require user alvaro**



[Ver ejercicio/ejemplo aqui](https://github.com/alvbencor/DESPLIEGUE/blob/main/ServidoresWeb/ejercicio10.md)


[↑ INDEX](#index)<br>

## <a name="htaccess">Autenticacion con htaccess</a>

Otra manera de configurar la autenticacion es creando el fichero **.htaccess** que se almacena detro de la carpeta que se quiere proteger. Esta opcion supone tener que modificar la configuracion general de apache para permitir que las propiedades sobre el directorio raiz puedan ser modificadas. El cambio que hay que realizar es sobre la directiva **AllowOverride**, que se establecera a **All**, permitiendo que la política de dicho directorio sea diferente si así se define con algun fichero *.htaccess*.

    <Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>


Y ya en el directorio que se quiere proteger, se incluye un fichero *.htaccess* con el siguiente contenido:


    AuthType Basic
    AuthName "Acceso restringido a monguers"
    AuthUserFile /etc/apache2/.htpasswd
    Require user fati



[↑ INDEX](#index)<br>

## <a name="error">Personalizar las páginas de error</a>

Basta con crear las paginas de error HTML que se quiera que vea el usuario y asociarlo al error que se quiera mostrar. 

Editamos el archivo **mipaginadeejemplo.com.conf:**


    nano /etc/apache2/sites-available/mipaginadewjwmplo.com.conf
    

Y editamos el contenido:

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

Las directivas **ErrorDocument** se pueden meter tambien en el fichero .htaccess siempre y cuando **AllowOverride sea All**


[↑ INDEX](#index)<br>


## <a name="ssl">Configurar SSL/TSL en Apache</a>

## Configurar SSL/TLS en Apache

**Secure Socket Layer** es un protocolo de seguridad cuyas diversas vulnerabilidades hicieron que fuera paulatinamente sustituido por el protocolo TLS (Transport Secure Layer).

Se ha hablado también del certificado necesario para poder establecer una conexion segura con TLS. Aunque los certificados los podemos crear nosotros, no son aceptados por los navegadores. 

Para crear un certificado, hay que crearlo con una clave. Se almacenan en el directorio **/etc/apache2/certs** que tenemos que crear nosotros mismos primero.
    
    openssl req -x509 -nodes -days 365 -newKey rsa:2048 -keyout /etc/apache2/certs/apache2.key -out /etc/apache2/certs/apache2.crt
    

Al ejecutar este comando y tras la introduccion de algunos datos que se solicitaran, se creara el certificado y su clave.

Tras esto, se activará el modulo ssl como hemos visto antes y se reiniciará apache. 

Una vez configurada la seguridad, hay que configurar los host virtuales a los que se quiera aplicar la misma. las acciones a realizar son: 
- Cambiar el puerto donde escucha al **443**
- Activar el soporte para SSL
- Indicar dónde estan el certificado y la clave.

Editamos el archivo:

    sudo nano /ect/apache2/sitas-available/mipaginaejemplo.com.conf
    
Y añadimos:

    ...
        </Directory>

        SSLEngineOn
            SSLCertificateFile /etc/apache2/certs/apache2.crt
            SSLertificateKeyFile /etc/apache2/certs/apache2.key
        SSLProtocol All -SSLv3
    </VirtualHost>
    
Ver [Ejercicio 11](https://github.com/alvbencor/DESPLIEGUE/blob/main/ServidoresWeb/ejercicio11.md)
    

[↑ INDEX](#index)<br>














  

  
