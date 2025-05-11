<script setup>
    import { ref } from "vue";
    import { defineEmits } from 'vue'

    const fechaCorta = ref([""]);  //fechas del calendario
    const fechaLarga = ref([""]);  //fechas del calendario
    const mesActual = ref(); //Mes actual del calendario mostrado
    const ultimoDiaSemana = ref();  //ultimo dia (Date) de la semana mostrado en calendario
    //Fecha del mes
    const mes = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']

    //Enviamos ultimoDiaSemana
    const emit = defineEmits(['miEvento'])
    const emitirEvento = () => {
      const fechas = [
      fechaLarga.value, 
      fechaCorta.value
      ]
      emit('miEvento', fechas)
    }
    /*
    * Añade los dias de la semana requerida para reservar
    * Mostrados en el mes y en el selector
    *
    */
    function FechaSemanal(fechaActual) {
        mesActual.value = fechaActual.getMonth();

        let diaDeLaSemana = fechaActual.getDay(); //0 domingo, 1 lunes...
        let dia = [0, 0, 0, 0, 0, 0, 0];

        //Restamos los dias
        for(let i=0; i < diaDeLaSemana; i++){
            if(i != diaDeLaSemana)
            dia[i] = (diaDeLaSemana-i)*-1;
        }

        //Sumamos los dias
        for(let i=diaDeLaSemana; i < 7; i++){
            if(i != diaDeLaSemana)
            dia[i] = diaDeLaSemana + i;
        }

        for(let i=0; i < 7; i++){
            let fechaActualTemp = new Date(fechaActual);
            fechaLarga.value[i] = fechaActualTemp.setDate(fechaActualTemp.getDate() + dia[i]);

            if(i==6)
                ultimoDiaSemana.value = new Date(fechaActualTemp);
            
            fechaCorta.value[i] =
            fechaActualTemp.toLocaleDateString("es-CL", {
                day: "numeric", // 2-digit
                month: "short" // numeric, 2-digit, narrow, long
            });
        }
    }

    const botonAnterior = () => {
    let fechaActualTemp = new Date(ultimoDiaSemana.value);
    fechaActualTemp.setDate(fechaActualTemp.getDate() - 7);
    FechaSemanal(fechaActualTemp);
    emitirEvento()
    };

    const botonSiguiente = () => {
    let fechaActualTemp = new Date(ultimoDiaSemana.value);
    fechaActualTemp.setDate(fechaActualTemp.getDate() + 1);
    FechaSemanal(fechaActualTemp);
    emitirEvento()
    };

    const fechaActual = new Date();
    FechaSemanal(fechaActual);
</script>

<template>
    <div v-bind:class="['contenedor-tabla']">
    
    <div v-bind:class="['contenedor-boton-Calendar']">
        <h2>{{ mes[mesActual] }}</h2>
        <button @click="botonAnterior">< Anterior</button>
        <button @click="botonSiguiente">Siguiente ></button>
    </div>
      <table>
        <tbody>
          <tr>
            <th>Horario</th>
            <th>Lunes<br>{{ fechaCorta[1] }}</th>
            <th>Martes<br>{{ fechaCorta[2] }}</th>
            <th>Miercoles<br>{{ fechaCorta[3] }}</th>
            <th>Jueves<br>{{ fechaCorta[4] }}</th>
            <th>Viernes<br>{{ fechaCorta[5] }}</th>
          </tr>
          <tr>
            <td>08:00 - 09:30</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
          </tr>
          <tr>
            <td>09:45 - 11:15</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
          </tr>
          <tr>
            <td>11:30 - 13:00</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
          </tr>
          <tr>
            <td>14:00 - 15:30</td>
            <td>6B<br>Matematicas<br>Carla Nail</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td>6B<br>Matematicasss<br>Carla Nail</td>
            <td><br>Libre<br><br></td>
          </tr>
        </tbody>
      </table>

    </div>
</template>

<style>
    .contenedor-boton-Calendar{
        display: flex; 
        align-items: center; 
        gap: 10px;
    }

    table {
        table-layout: fixed;
        width: 700px;
        height: 400px;
        border: 1px;
        border: 0 solid #e5e7eb;
        border-collapse: collapse;
    }

    th {
        background-color: rgba(82, 148, 192, 0.864);
        text-align: center;
        border: 1px solid rgb(160 160 160);
        border-collapse: collapse;
    }

    td {
        text-align: center;
        border: 1px solid rgb(160 160 160);
        border-collapse: collapse;
    }

    button {
        width: 130px;
        height: 40px;
        color: rgb(148 163 184/var(--tw-text-opacity,1));
        border-radius: 8px;
        border: 1px solid transparent;
        padding: 0.6em 1.2em;
        font-size: 1em;
        font-weight: 500;
        font-family: inherit;
        cursor: pointer;
        transition: border-color 0.25s;
    }

    h2{
      color: rgb(148 163 184/var(--tw-text-opacity, 1));
    }
</style>