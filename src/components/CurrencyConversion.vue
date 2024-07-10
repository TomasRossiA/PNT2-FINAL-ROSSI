<template>
  <div class="container mt-5">
    <div class="card p-4 bg-light">
      <h1 class="text-center mb-4">Conversión de Pesos a Dólares</h1>
      <div class="form-group">
        <label for="pesos">Pesos:</label>
        <input v-model.number="pesos" type="number" id="pesos" class="form-control" placeholder="Ingresa cantidad en pesos">
      </div>
      <div class="form-group">
        <label for="cotizacion">Cotización del Dólar:</label>
        <input v-model.number="cotizacion" type="number" id="cotizacion" class="form-control" :disabled="autoUpdate">
      </div>
      <div class="form-group">
        <label for="resultado">Resultado en Dólares:</label>
        <input :value="resultado" type="number" id="resultado" class="form-control" disabled>
      </div>
      <div class="form-check mb-4">
        <input type="checkbox" id="autoUpdate" v-model="autoUpdate" class="form-check-input">
        <label for="autoUpdate" class="form-check-label">Actualizar cotización automáticamente</label>
      </div>
      <p class="text-muted">Última actualización: {{ lastUpdated }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'CurrencyConversion',
  data() {
    return {
      pesos: 0,
      cotizacion: 0,
      autoUpdate: false,
      lastUpdated: null,
      intervalId: null
    };
  },
  computed: {
    resultado() {
      return (this.pesos / this.cotizacion).toFixed(2);
    }
  },
  watch: {
    autoUpdate(newValue) {
      if (newValue) {
        this.startAutoUpdate();
      } else {
        this.stopAutoUpdate();
      }
    }
  },
  methods: {
    async fetchCotizacion() {
      try {
        const response = await axios.get('https://api.bluelytics.com.ar/v2/latest');
        this.cotizacion = response.data.blue.value_sell;
        this.lastUpdated = new Date().toLocaleString();
      } catch (error) {
        console.error('Error fetching cotizacion:', error);
      }
    },
    startAutoUpdate() {
      this.fetchCotizacion();
      this.intervalId = setInterval(this.fetchCotizacion, 2000);
    },
    stopAutoUpdate() {
      if (this.intervalId) {
        clearInterval(this.intervalId);
        this.intervalId = null;
      }
    }
  },
  mounted() {
    this.fetchCotizacion();
  }
};
</script>

<style scoped>
.card {
  background-color: #f8f9fa;
}
</style>
