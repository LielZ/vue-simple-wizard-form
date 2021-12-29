<template>
  <div class="container">
    <Form />
  </div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: {
    Form
  }
}


</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Heebo:wght@100;200;300;400;500;600;700;800;900&display=swap');
#app {
  font-family: 'Heebo', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #161616;
  margin-top: 10px;
}
</style>
