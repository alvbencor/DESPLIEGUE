<template>

<h1>Gestor de tareas</h1>
  
  <Formulario @enviarFormulario="datosFormulario"/>

  <table>

    <tbody>
      <tr><th>Tareas Pendientes</th>
      <th>Tareas en proceso</th>
      <th>Tareas para revisión</th>
      <th>Tareas revisadas</th></tr>

      <tr>
        <td> <div v-for="(item, index) in tareas" :key='index' class="">
            <div v-if="item.estado =='pendiente'" class="tituloTarea tarea pendiente ">
              <input type="checkbox" class="check" @change="cambiarEstado(item.nombre, item.estado)">
              <div class="descripcion">
                <h2>{{ item.nombre }}</h2>
                <p>{{ item.descripcion }}</p>
                </div>
              </div>
              
            </div>
          </td>

          <td> <div v-for="(item, index) in tareas" :key='index' class="">
            <div v-if="item.estado =='proceso'" class="tituloTarea tarea proceso">
              <input type="checkbox" class="check" @change="cambiarEstado(item.nombre, item.estado)">
              <div class="descripcion">
                <h2>{{ item.nombre }}</h2>
                <p>{{ item.descripcion }}</p>
                </div>
              </div>
              
            </div>
          </td>

          <td> <div v-for="(item, index) in tareas" :key='index' class="">
            <div v-if="item.estado =='revision'" class="tituloTarea tarea revision">
              <input type="checkbox" class="check" @change="cambiarEstado(item.nombre, item.estado)">

              <div class="descripcion">
                <h2>{{ item.nombre }}</h2>
                <p>{{ item.descripcion }}</p>
                </div>
              </div>
              
            </div>
          </td>

          <td> <div v-for="(item, index) in tareas" :key='index' class="">
            <div v-if="item.estado =='revisado'" class="tituloTarea tarea revisado">
            
              <div class="descripcion">
                <h2>{{ item.nombre }}</h2>
                <p>{{ item.descripcion }}</p>
                </div>
              </div>
              
            </div>
          </td>
      </tr>

      


    </tbody>
  </table>

 




</template>

<script>

import Formulario from '@/components/Formulario.vue';


export default {
  name: 'App',
  components: {
    Formulario
  },
  data() {
    return {
      tareas: [{nombre: 'comer', descripcion: 'comer' , estado: 'pendiente' },
      {nombre: 'salir', descripcion: 'tarde' , estado: 'proceso' },
      {nombre: 'dormir', descripcion: 'tarde' , estado: 'revision' },
      {nombre: 'saltar', descripcion: 'tarde' , estado: 'revisado' }

      
      
      ]
    }
  },
  methods: {

  datosFormulario(nombre, descripcion){

        if (!descripcion==""){

          let objNuevo={nombre: nombre, descripcion: descripcion, estado: 'pendiente'}

          this.tareas.push(objNuevo)

        console.log(this.tareas)

  } else console.log("por favor, introduzca descripcion");


  

},
cambiarEstado(nombre, estado){

  for (let i=0; i< this.tareas.length;i++){


    if(this.tareas[i].nombre == nombre && this.tareas[i].estado == 'pendiente'){

      this.tareas[i].estado = 'proceso';

    } else if(this.tareas[i].nombre == nombre && this.tareas[i].estado == 'proceso'){

    this.tareas[i].estado = 'revision';

    } else if(this.tareas[i].nombre == nombre && this.tareas[i].estado == 'revision'){

    this.tareas[i].estado = 'revisado';

    } else this.tareas[i].estado == 'revisado';

  
    
  }
}


},
computed: {
  arrayProceso() {
      // return this.tareas.filter((item, index) => index.estado === 'proceso');
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
 
  color: #2c3e50;
  margin-top: 60px;
}

table{
  width: 80%;
  margin: 3rem auto;

}

.tarea{
  
  padding: 1rem;
  margin-bottom: 1rem;
}
.tituloTarea{
  display: flex;
  gap: 1rem;

}

.descripcion{
  margin: 0;
  padding: 0;
}

.pendiente{
  background-color: rgb(246, 101, 101);
}

.proceso{
  background-color: rgb(254, 200, 64);

}

.revision{
  background-color: rgb(232, 243, 114);

}

.revisado{
  background-color: rgb(172, 255, 133);

}

td{

  
  
}


</style>
