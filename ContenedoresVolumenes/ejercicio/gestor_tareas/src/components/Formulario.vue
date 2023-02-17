<template lang="">
    <div>


        <div class="caja">
            <form action="" @sumbit.prevent class="formulario">

                <input type="text" placeholder="Nueva tarea" v-model="nombre">

                <div class="text">
                    <textarea name="" id=""  rows="10" placeholder="Descripción de la tarea" v-model="descripcion"></textarea>
                    <p :v-if="descripcion ==''">Este campo es obligatorio</p>
                  
                </div>
                
                

                <button @click="enviar" type="submit">Crear nueva tarea</button>
            </form>
        </div>
    </div>
</template>
<script>
export default {

    emits:['enviarFormulario'],
    data(){

    return{

      nombre:"",
      descripcion:"",
      
        
    }

  },
  methods: {
    enviar() {
      this.$emit('enviarFormulario', 
      this.nombre,  this.descripcion
      )
    }
  },

    
    
}
</script>
<style scooped>

    .caja{

        background-color: rgb(219, 221, 220);
    }

    .formulario{
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        width: 40%;
     
       
        padding: 2rem;
        gap: 2rem;

    }

    input, textarea, button {
        padding: .5rem;
        border-radius: .5rem;
        border: 1px solid #ccc;
    }

    button{
        background-color: rgb(11, 112, 146);
        height: 3rem;
        text-transform: uppercase;
        font-weight: bold;
        color: rgb(235, 235, 247);
    }
    .text p{
        margin: 0;
        text-align: right;
        font-size: .8rem;
        color: red;
    }

    textarea {
        width: 100%;
        box-sizing: border-box;

    }

    


    
</style>