<template>
    <div class="container mt-4">
      <div class="row mb-3">
        <div class="col">
          <label for="numberInput1" class="form-label">Horas:</label>
          <input id="numberInput1" v-model.number="horas" type="number" min="0" class="form-control" />
        </div>
        <div class="col">
          <label for="numberInput2" class="form-label">Minutos:</label>
          <input id="numberInput2" v-model.number="minutos" type="number" min="0" class="form-control" />
        </div>
        <div class="col">
          <label for="numberInput3" class="form-label">Segundos:</label>
          <input id="numberInput3" v-model.number="segundos" type="number" min="0" class="form-control" />
        </div>
      </div>
  
      <div class="text-center mb-3">
        <h3>Tiempo restante:</h3>
        <h2> <span class="badge bg-primary">{{ horasDisplay }}:{{ minutosDisplay }}:{{ segundosDisplay }}</span></h2>
      </div>
  
      <div v-if="mensajeVisible" class="alert alert-success text-center" role="alert">
        <img src="../assets/img/despertador-12.gif" alt="Alerta" class="mb-2" />
        <div>¡Tiempo terminado!</div>
      </div>
  
      <div class="text-center">
        <button class="btn btn-primary me-2" @click="inicio">Iniciar</button>
        <button class="btn btn-danger" @click="cancelarRegresiva">Cancelar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        horas: 0,
        minutos: 0,
        segundos: 0,
        tiempoRestante: 0,
        regresiva: null,
        mensajeVisible: false, // Controla la visibilidad del mensaje
      };
    },
    computed: {
      horasDisplay() {
        return Math.floor(this.tiempoRestante / 3600).toString().padStart(2, "0");
      },
      minutosDisplay() {
        return Math.floor((this.tiempoRestante % 3600) / 60).toString().padStart(2, "0");
      },
      segundosDisplay() {
        return (this.tiempoRestante % 60).toString().padStart(2, "0");
      },
    },
    methods: {
      inicio() {
        this.mensajeVisible = false; // Oculta el mensaje al iniciar
        this.tiempoRestante = this.horas * 3600 + this.minutos * 60 + this.segundos;
  
        if (this.tiempoRestante > 0) {
          clearInterval(this.regresiva);
          this.regresiva = setInterval(this.actualizaTiempo, 1000);
        }
      },
      actualizaTiempo() {
        if (this.tiempoRestante <= 0) {
          clearInterval(this.regresiva);
          this.mensajeVisible = true; // Muestra el mensaje cuando termina
          this.resetearRegresiva();
          return;
        }
  
        this.tiempoRestante--;
      },
      cancelarRegresiva() {
        clearInterval(this.regresiva);
        this.resetearRegresiva();
      },
      resetearRegresiva() {
        this.horas = 0;
        this.minutos = 0;
        this.segundos = 0;
        this.tiempoRestante = 0;
      },
    },
  };
  </script>
  
  <style>
  .container {
    max-width: 600px;
  }
  input {
    width: 50px;
    margin-right: 10px;
  }
  h2 {
    margin-bottom: 20px;
    font-size: 100px;
  }
  </style>
  