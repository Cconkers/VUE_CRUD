<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Editar Empleado</div>
      <div class="card-body">
        <form v-on:submit.prevent="actualizarRegistro()">
          <div class="form-group">
            <label for="nombre">Nombre</label>
            <input
              required
              v-model="empleado.nombre"
              type="text"
              class="form-control"
              id="nombre"
              name="nombre"
              placeholder="Escribe el nombre del empleado"
              aria-describedby="helpId"
            />
          </div>

          <div class="form-group">
            <label for="correo">Correo</label>
            <input
              required
              v-model="empleado.correo"
              type="text"
              id="correo"
              name="correo"
              class="form-control"
              placeholder="Escribe el correo electrónico del empleado"
              aria-describedby="helpId"
            />
          </div>

          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-success">Modificar</button>

            <router-link :to="{ name: 'Listar' }" class="ml-1 btn btn-warning"
              >Cancelar</router-link
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return {empleado:{}
        }
},

created:function(){
    this.editarEmpleados();
},

methods:{

    editarEmpleados() {
      fetch("http://localhost/empleados/?consultar="+this.$route.params.id)
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
            console.log(datosRespuesta)
            this.empleado=datosRespuesta[0];
        })
        .catch(console.log)
    },

    actualizarRegistro(){
        var datosEnviar = {id:this.$route.params.id,
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };
      console.log(datosEnviar);
      fetch("http://localhost/empleados/?actualizar="+this.$route.params.id, {
        method: "POST",
        body: JSON.stringify(datosEnviar),
      })
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          console.log(datosRespuesta);
          window.location.href = "../listar";
        })
    }

}

}
</script>
