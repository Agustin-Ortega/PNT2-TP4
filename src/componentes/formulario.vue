<template >

  <section class="src-componentes-formulario">
    <div class="jumbotron">

      <div id="jumbotron2" class="jumbotron">
        <h1>Formulario de Usuarios</h1>
        <hr><br>
        <div id="jumbotron3" class="jumbotron">

          <vue-form :state="formState" @submit.prevent="enviar()">

            <validate tag="div">

              <label for="nombre">Nombre</label>
              <input type="text" id="nombre" class="form-control" autocomplete="off" v-model.trim="Datos.nombre"
                name="nombre" required :minlength="nombreMinLength" :maxlength="nombreMaxLength" no-espacios>

              <!-- VALIDACIONES -->
              <field-messages name="nombre" show="$dirty">
                <div lass="font">Bienvenido/a {{ Datos.nombre }}</div>
                <div slot="required" class="alert alert-danger mt-1">Campo Nombre requerido</div>
                <div slot="minlength" class="alert alert-warning mt-1">Este campo debe poseer al menos {{
                    nombreMinLength
                }}
                  caracteres.</div>
                <!-- VALIDACIONES -->
                <div slot="no-espacios" class="alert alert-danger mt-1">El campo no permite espacios intermedios.</div>
              </field-messages>

            </validate><br>
            <hr>


            <validate tag="div">

              <label for="edad">Edad</label>
              <input type="number" id="edad" class="form-control" autocomplete="off" v-model.number="Datos.edad"
                name="edad" required :min="edadMin" :max="edadMax">
              <!-- VALIDACIONES -->
              <field-messages name="edad" show="$dirty">
                <div class="font">Edad confirmada</div>
                <div slot="required" class="alert alert-danger mt-1">Campo edad requerido</div>
                <div slot="min" class="alert alert-warning mt-1">La edad minima debe ser {{ edadMin }} años.</div>
                <div slot="max" class="alert alert-warning mt-1">La edad maxima debe ser {{ edadMax }} años.</div>
              </field-messages>

            </validate><br>
            <hr>


            <validate tag="div">

              <label for="email">Email</label>
              <input type="email" id="email" class="form-control" autocomplete="off" v-model.trim="Datos.email"
                name="email" required>
              <!-- VALIDACIONES -->
              <field-messages name="email" show="$dirty">
                <div class="font">Acceso concedido</div>
                <div slot="required" class="alert alert-danger mt-1">Campo email requerido</div>
                <div slot="email" class="alert alert-danger mt-1">Email no valido</div>
              </field-messages>

            </validate><br>

            <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>
          </vue-form>
        </div>
      </div>


      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>

          <td v-if="!Datos.nombre">-</td><td v-else>{{Datos.nombre}}</td>
          <td v-if="!Datos.edad">-</td><td v-else-if="Datos.edad < 120 && Datos.edad >5">{{ Datos.edad }}</td><td v-else>Edad fuera de rango</td>
          <td v-if="!Datos.email">-</td><td>{{ Datos.email }}</td>

        </table>
      </div>
    </div>
  </section>
</template>

<script >

export default {
  name: 'src-componentes-formulario',
  props: [],
  mounted() {

  },
  data() {
    return {
      hayDatos: this.datos.nombre,
      formState: {},
      Datos: this.datos(),
      nombreMinLength: 5,
      nombreMaxLength: 15,
      edadMin: 18,
      edadMax: 120,
    }
  },
  methods: {
    datos() {
      return {
        nombre: null,
        edad: null,
        email: null,
      }
    },

    enviar() {
      this.Datos = this.datos()
      this.formState._reset();
    }
  },
  computed: {
    getNombre() {
      return this.datos.nombre;
    },
    getEdad() {
      return this.datos.edad;
    },
    getEmail() {
      return this.datos.email;
    }
  }
}


</script>

<style scoped lang="css">
#jumbotron3 {
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  font-size: 1.3rem;
  color: rgb(68, 6, 6);
  background-color: rgba(250, 235, 215, 0.932);
}

hr {
  color: antiquewhite;
}

#jumbotron2 {
  color: antiquewhite;
  background-color: rgb(68, 6, 6);
}

td {
  color: antiquewhite;
  font-size: large;
  text-align: center;
  background-color: rgb(68, 6, 6);
  padding-bottom: 1.8rem;
}

th {
  text-align: center;
}
</style>
