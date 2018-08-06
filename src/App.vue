<template>
  <div class="principal">
    <div class="logo">
      <a href="index.html">
        <img src="/static/logo.png" alt="Liber">
      </a>
    </div>

    <formulario></formulario>

  </div>
</template>

<script>

  import Formulario from './components/shared/Formulario.vue';

  export default {
    components: {
      'formulario' : Formulario,
    },
    name: 'app'
}

</script>
