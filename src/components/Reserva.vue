
<script setup>
  import { ref } from 'vue'

  const nombre = ref('')
  const curso = ref('')
  const asignatura = ref('')
  const laboratorio = ref('')
  const horario = ref('')
  const dia = ref('')

  const enviarFormulario = () => {
    console.log({
      nombre: nombre.value,
      curso: curso.value,
      asignatura: asignatura.value,
      laboratorio: laboratorio.value,
      horario: horario.value,
      dia: dia.value
    })
  }

  const props = defineProps({
    mensaje: String
  })
</script>
  
<template>
  <form @submit.prevent="enviarFormulario" style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; max-width: 600px;">
    <!-- Columna 1 -->
    <div>
      <input v-model="nombre" type="text" placeholder="Nombre" style="width: 100%;" />
    </div>
    <!-- Columna 2 -->
    <div>
      <select v-model="laboratorio" style="width: 100%;">
        <option disabled value="">Selecciona Laboratorio</option>
        <option>Lab 1</option>
        <option>Lab 2</option>
        <option>Lab 3</option>
      </select>
    </div>

    <div>
      <input v-model="curso" type="text" placeholder="Curso" style="width: 100%;" />
    </div>
    <div>
      <select v-model="horario" style="width: 100%;">
        <option disabled value="">Selecciona Horario</option>
        <option>08:00 - 10:00</option>
        <option>10:00 - 12:00</option>
        <option>14:00 - 16:00</option>
      </select>
    </div>

    <div>
      <input v-model="asignatura" type="text" placeholder="Asignatura" style="width: 100%;" />
    </div>
    <div>
      <select v-model="dia" style="width: 100%;">
        <option disabled value="">Selecciona Día</option>
        <option>Lunes</option>
        <option>Martes</option>
        <option>Miércoles</option>
        <option>Jueves</option>
        <option>Viernes</option>
      </select>
    </div>

    <!-- Botón ocupa las dos columnas -->
    <div style="grid-column: span 2; text-align: center;">
      <button type="submit">Enviar</button>
    </div>
  </form>

  <span>Mensaje recibido: {{ mensaje[1] }}</span>
</template>


