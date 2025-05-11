<script setup>
  import { ref } from 'vue';
  import Calendario from './components/Calendario.vue';
  import Reserva from './components/Reserva.vue';

  const mensaje1ParaHijoB = ref('')

  const manejarEvento = (fechas) => {
    console.log('Evento recibido:', fechas[0]);
    console.log('Evento recibido:', fechas[1]);
    mensaje1ParaHijoB.value = fechas;
  }

</script>

<template>
    <div class="max-w-xl mx-auto p-4">
      <h1>Reserva de Laboratorio</h1>
      <Calendario @miEvento="manejarEvento"/>
    </div>
    <Reserva :mensaje="mensaje1ParaHijoB"/>
</template>

<style>
  body{
    background-color: rgb(255 255 255 / var(--tw-bg-opacity,1));
    color: rgb(148 163 184/var(--tw-text-opacity,1));
  }

  h1 {
    font-size: 3.2em;
    line-height: 0;
  }
</style>