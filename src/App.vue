<template>
  <div id="app">
    <CurrencyConversion />
    <div class="container mt-5">
      <h2 class="text-center mb-4">Preguntas y Respuestas</h2>
      <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Pregunta</th>
            <th scope="col">Respuesta</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>¿Qué es Axios?</td>
            <td class="text-success">b) Es una biblioteca de cliente http</td>
          </tr>
          <tr>
            <td>¿Cuál es la forma correcta para registrar un evento de click en Vue.js?</td>
            <td class="text-success">b) @click</td>
          </tr>
          <tr>
            <td>Con Axios se pueden implementar los verbos:</td>
            <td class="text-success">c) Get, Post, Put y Delete</td>
          </tr>
          <tr>
            <td>¿Cuál de estas directivas se utiliza para modificar estilos a través de Vue.js?</td>
            <td class="text-success">b) v-bind:style</td>
          </tr>
          <tr>
            <td>¿Qué función cumple el modificador number aplicado a v-model?</td>
            <td class="text-success">a) Permite transformar la entrada de un elemento en un número</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import CurrencyConversion from './components/CurrencyConversion.vue';

export default {
  name: 'App',
  components: {
    CurrencyConversion
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.table-striped tbody tr:nth-of-type(odd) {
  background-color: rgba(0, 0, 0, 0.05);
}

.text-success {
  color: #28a745 !important;
}
</style>
