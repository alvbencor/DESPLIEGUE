## ejercicio 3  

Desarrolla(o utiliza una que ya tengas) una aplicación que solicite datos a alguna 
API externa( a la API JSonPlaceHolder servirá).(Por ejemplo, el ejercicio del 
periódico con Vue-Router es suficiente).Crea una imagen para dicha aplicación, ejecuta un contenedor de la misma y 
comprueba que la aplicación funciona y carga los datos solicitados a la API. Crea un fichero .json y copia en el el contenido de la API a la que estabas llamando 
en el punto anterior. Arranca el servidor local json-server para que sirva los datos 
que acabas de incluir en el fichero .json.
. Modifica el código de tu aplicación para que, tras regenerar la imagen, la 
aplicación siga funcionando pero solicitando los datos al servidor local json-server.

Para cumplir con este ejercicio, utilizaremos la API gratuita JSONPlaceholder, que nos proporciona datos de ejemplo para hacer pruebas con peticiones HTTP. También utilizaremos Vue.js para crear la aplicación y Docker para crear y ejecutar el contenedor de la misma.

Paso 1: Crear la aplicación
Para comenzar, crearemos una nueva aplicación de Vue.js utilizando Vue CLI. Para ello, abrimos una terminal y escribimos el siguiente comando:

    vue create my-app

Esto creará una nueva aplicación de Vue.js llamada my-app. A continuación, nos movemos al directorio de la aplicación y añadimos el módulo axios para realizar peticiones HTTP a la API. Para ello, escribimos el siguiente comando:


    cd my-app
    npm install axios --save
    
    
A continuación, editamos el archivo src/App.vue y añadimos el siguiente código:

    html
    Copy code
    <template>
      <div>
        <h1>Posts</h1>
        <ul>
          <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
        </ul>
      </div>
    </template>

    <script>
    import axios from 'axios'

    export default {
      data() {
        return {
          posts: []
        }
      },
      created() {
        axios.get('https://jsonplaceholder.typicode.com/posts')
          .then(response => {
            this.posts = response.data
          })
          .catch(error => {
            console.log(error)
          })
      }
    }
    </script>
    
    
Este código crea una lista de elementos HTML que muestra los títulos de los posts obtenidos de la API de JSONPlaceholder utilizando axios.

Para comprobar que la aplicación funciona correctamente, abrimos una terminal en el directorio my-app y escribimos el siguiente comando para ejecutar la aplicación en modo de desarrollo:

    npm run serve
    
    
Luego, abrimos nuestro navegador web en la dirección http://localhost:8080 y deberíamos ver la lista de títulos de los posts de la API.

Paso 2: Crear la imagen y ejecutar el contenedor
Ahora, crearemos una imagen de Docker para nuestra aplicación y ejecutaremos un contenedor a partir de ella. Para ello, creamos un archivo llamado Dockerfile en el directorio raíz de la aplicación con el siguiente contenido:


#### Usa la imagen oficial de node como base

    FROM node:12-alpine

#### Establece el directorio de trabajo en /app


    WORKDIR /app

#### Copia los archivos del proyecto al contenedor

    COPY package*.json ./
    COPY . .

#### Instala las dependencias del proyecto

    RUN npm install

#### Construye la aplicación para producción

    RUN npm run build

####  Expone el puerto 8080

    EXPOSE 8080

####  Ejecuta el comando "npm start" cuando se inicie el contenedor

    CMD [ "npm", "start" ]
    
Este archivo define una imagen de Docker que utiliza la imagen oficial de Node.js como base, copia los archivos de la aplicación en el contenedor, instala las dependencias y construye la aplicación para producción. Luego, expone el puerto 8080 y ejecuta el comando npm start cuando se inicie el contenedor.

A continuación, abrimos una terminal en el directorio raíz de la aplicación y ejecutamos el siguiente comando para construir la imagen de Docker:


    docker build -t my-app .
    Esto creará una




alvaro benito
construye ella imagen de docker y el contenedor
Continuando desde el paso anterior, una vez que hemos construido la imagen de Docker utilizando el comando docker build -t my-app ., podemos ejecutar un contenedor a partir de ella utilizando el siguiente comando:

css
Copy code
docker run -p 8080:8080 my-app
Este comando ejecuta un contenedor a partir de la imagen my-app, expone el puerto 8080 del contenedor al puerto 8080 del host y ejecuta el comando npm start dentro del contenedor.

Una vez que el contenedor está en ejecución, podemos abrir nuestro navegador web en la dirección http://localhost:8080 y deberíamos ver la lista de títulos de los posts de la API.

Paso 3: Crear y servir el archivo .json
Para crear y servir un archivo JSON localmente, podemos utilizar la herramienta json-server. Esta herramienta nos permite crear un servidor web que sirve un archivo JSON como si fuera una API REST.

Para ello, creamos un archivo llamado db.json en el directorio raíz de la aplicación con el siguiente contenido:

json
Copy code
{
  "posts": [
    {
      "id": 1,
      "title": "Post 1",
      "body": "Lorem ipsum dolor sit amet."
    },
    {
      "id": 2,
      "title": "Post 2",
      "body": "Consectetur adipiscing elit."
    },
    {
      "id": 3,
      "title": "Post 3",
      "body": "Sed do eiusmod tempor incididunt."
    }
  ]
}
Este archivo define una lista de tres posts de ejemplo.

A continuación, instalamos json-server utilizando el siguiente comando:

Copy code
npm install -g json-server
Una vez que json-server está instalado, podemos ejecutarlo utilizando el siguiente comando:

css
Copy code
json-server --watch db.json
Este comando crea un servidor web que sirve el archivo db.json en la dirección http://localhost:3000.

Paso 4: Modificar la aplicación para utilizar el servidor local
Por último, podemos modificar la aplicación para que utilice el servidor local de json-server en lugar de la API de JSONPlaceholder. Para ello, editamos el archivo src/App.vue y reemplazamos el código existente con el siguiente:

html
Copy code
<template>
  <div>
    <h1>Posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      posts: []
    }
  },
  created() {
    axios.get('http://localhost:3000/posts')
      .then(response => {
        this.posts = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>
Este código utiliza axios para obtener los posts del servidor local de json-server en lugar de la API de JSONPlaceholder.

Para probar que la aplicación funciona correctamente con el servidor local, debemos construir una nueva imagen de Docker que incluya los cambios utilizando el comando docker build -t my-app ., y luego ejecutar un nuevo contenedor a partir de ella utilizando el comando docker run -p 8080:8080 my-app.

Una vez que el nuevo contenedor está en ejecución, podemos abrir nuestro navegador web en la dirección http://localhost:8080 y
