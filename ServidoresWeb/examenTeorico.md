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


  

  
