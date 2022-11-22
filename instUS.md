# Instalación de Ubuntu Server 22.04 en virtual box
## Interfaz gráfica

Instalaremos el escritorio **MATE**.

Instalar tasksel

    sudo apt-get install tasksel
  
Instalar escritorio MATE

    sudo tasksel


Nos movemos con las flechas y seleccionamos  [ * ] MATE con la barra espaciadora.




Reiniciamos

    sudo reboot

## Instalación Guest Additions

    sudo apt update
    sudo apt upgrade
    
En configuracion de la máquina > almacenamiento, en el controlador IDE cargamos el ISO de las guest additions
En el escritorio saldrá un mensaje para ejecutar el disco que acabamos de montar. Le decimos que sí, e instalará las guest additions.

Reiniciamos y ya deberíamos tener las guestAdditions instaladas. 

    sudo reboot
    



  
