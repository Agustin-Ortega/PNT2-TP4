<template >

  <section class="src-componentes-inicio">
    <div class="jumbotron">
    <H4>Proyecto TP 4 </H4><hr>
    <P>1) Un formulario basado en vue-form que contenga 3 campos: nombre, edad e email. Este debe
      tener validaciones mediante carteles de: campos requeridos, nombre entre 5 y 15 caracteres, edad
      entre 18 y 120 años e email válido. Los datos válidos ingresados por el formulario, se deben
      representar en un tabla por debajo del mismo, en el mismo momento del ingreso.
    </P>
    <p>
      2) Realizar un componente que pida los objetos almacenados en un recurso de mockapi.io llamado
      usuarios, que contengan datos aleatorios con las claves: nombre, email y número de teléfono. Se
      representarán en una tabla en la vista.
    </p><br>
    <p align="center">XMLHttpRequest, fetch y axios.</p><p>Agustin Ortega</p>
    </div>
  </section>

</template>

<script >

  export default  {
    name: 'src-componentes-inicio',
    props: [],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-inicio {

  }
</style>
