<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Agregar Nuevo Empleado</div>
      <div class="card-body">
        <form v-on:submit.prevent="agregarRegistro()">
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
            <button type="submit" class="btn btn-success">Agregar</button>

            <router-link :to="{ name: 'Listar' }" class="btn btn-warning"
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
  data() {
    return {
      empleado: {},
    };
  },
  methods: {
    agregarRegistro() {
      var datosEnviar = {
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };
      console.log(datosEnviar);
      fetch("http://localhost/empleados/?insertar=1", {
        method: "POST",

        body: JSON.stringify(datosEnviar),
      })
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          console.log(datosRespuesta);
          window.location.href = "listar";
        })
        .catch(function () {
          var audio = new Audio(
            "https://rpg.hamsterrepublic.com/wiki-images/d/d7/Oddbounce.ogg"
          );
          audio.play();
          alert("ERROR FATAL");
        });
    },
  },
};
</script>
