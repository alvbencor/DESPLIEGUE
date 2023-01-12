# Docker II

## Comandos parar procesos en terminal mac

#### Comprobar puertos abiertos en terminal mac

    lsof -i -P | grep -i listen

#### Comprobar que aplicación usa el puerto 8080
    lsof -i -P|grep -i "8080"
    
#### Matar proceso

> MacBook-Pro-de-Alvaro:dawes-varios alvarobenitocortes$ lsof -i -P|grep -i "8080"<br>
java      **99618** alvarobenitocortes   39u  IPv6 0xb8b1bc3dfba578ef      0t0  TCP *:8080 (LISTEN)<br>
<br>
En este caso: kill -9 `99618` <br>


    kill -9 numero-id
    
    


## Comandos Docker


#### docker sbom

Para saber qué hay dentro de las imágenes

El nuevo comando `docker sbom` CLI muestra el SBOM (Software Bill Of Materials) de cualquier imagen de Docker. 
Saca el SBOM en una tabla o lo exporta en formato SPDX y CycloneDX.
