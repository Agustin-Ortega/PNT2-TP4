<template >
  <section class="src-componentes-usuarios-mock-api">
    <div class="jumbotron">

      <div align="center">
        <button class="btn btn-warning my-3 mr-3" @click="getXHR()">XHR Callback</button>
        <button class="btn btn-warning my-3 mr-3" @click="getXHRPromise()">XHR Promise</button>
        <button class="btn btn-info my-3 mr-3" @click="getFetch()">Fetcht</button>
        <button class="btn btn-info my-3 mr-3" @click="getAxios()">Axios</button><br>
        <button class="btn btn-danger my-3 mr-3" @click="borrar">Borrar</button><br>
        <hr>
      </div>

      <div v-if="posts.length" align="center" class="fun">
        Funcion {{ met }}
      </div>

      <div v-if="posts.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Telefono</th>
          </tr>
          <tr v-for="post in posts" :key="post.id">
            <td>{{ post.nombre }}</td>
            <td>{{ post.email }}</td>
            <td>{{ post.numero }}</td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-warning text-center">Lista Vacia</h4>
    </div>
  </section>

</template>

<script >

export default {
  name: 'src-componentes-usuarios-mock-api',
  props: [],
  mounted() {

  },
  data() {
    return {
      urlMock: 'https://6353835fe64783fa827433c7.mockapi.io/mock/usuarios',
      met: [],
      posts: []
    }
  },
  methods: {

    borrar() {
      this.posts = [],
        this.met = []
    },
    // CON XHR CON CALLBACK
    getXHR() {

      const xhr = new XMLHttpRequest()
      xhr.open('get', this.urlMock)
      xhr.addEventListener('load', () => {
        if (xhr.status == 200) {
          let respuesta = JSON.parse(xhr.response)
          this.posts = respuesta;
          this.met = 'XHR Callback'
        }
      })
      xhr.send()
    },

    // CON XHR CON PROMESAS
    xhrPromise() {
      return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest()
        xhr.open('get', this.urlMock)
        xhr.addEventListener('load', () => {
          if (xhr.status == 200) {
            let respuesta = JSON.parse(xhr.response)
            resolve(respuesta);
          }
          else {
            reject(xhr.status + 'Error en http')
          }
        })
        xhr.send()
      })
    },

    async getXHRPromise() {
      try {
        let respuesta = await this.xhrPromise()
        this.posts = respuesta;
        this.met = 'XHR Promise'
      }
      catch (error) {
        console.error(error);
      }
    },

    // CON FETCH
    async getFetch() {

      try {
        let response = await fetch(this.urlMock)
        let respuesta = await response.json()
        this.posts = respuesta;
        this.met = 'FETCH'
      } catch (error) {
        console.error(error);
      }

    },
    // CON AXIOS
    async getAxios() {
      try {
        let respuesta = await this.axios(this.urlMock)
        this.posts = respuesta.data;
        this.met = 'AXIOS'

      } catch (error) {
        console.error(error)
      }
    }
  },
  computed: {

  }
}


</script>

<style scoped lang="css">
.src-componentes-usuarios-mock-api {}

table {
  text-align: center;
}

td {
  color: rgb(95, 4, 4);
  background-color: antiquewhite;
  font-size: medium;
}

th {
  background-color: rgb(95, 4, 4);
  color: antiquewhite;
}

.fun {
  font-size: x-large;
  background-color: rgba(0, 0, 0, 0.651);
  color: antiquewhite;

}
</style>
