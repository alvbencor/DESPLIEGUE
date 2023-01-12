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

Do you know what's inside your image?


#### docker sbom
The new `docker sbom` CLI command displays the SBOM (Software Bill Of Materials) of any Docker image. This feature outputs the SBOM in a table or can be exported into SPDX and CycloneDX formats.
