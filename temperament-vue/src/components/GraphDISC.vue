<script setup>
import { ref } from 'vue';
import { Bar, Line } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale , LineElement, PointElement} from 'chart.js';
import TempD from './TempD.vue';
import TempI from './TempI.vue';
import TempS from './TempS.vue';
import TempC from './TempC.vue';
const emit = defineEmits(['continue', 'back']);

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, LineElement, PointElement);

const goBack = () => {
  emit('back');
}


const props = defineProps({
  DISC: {
    type: Array,
    default: () => [0, 0, 0, 0]
  }
});


const chartData = ref({
  labels: ['D', 'I', 'S', 'C'],
  datasets: [
    {
      label: 'Línea de Referencia', // Etiqueta para la línea
      backgroundColor: '#FF6384', // Color de los puntos
      borderColor: '#FF6384', // Color de la línea
      data: [30, 30, 30, 30], // Datos para la línea (valor fijo en 30)
      type: 'line', // Define el tipo de gráfico como línea
      fill: false, // No rellena el área debajo de la línea
      tension: 0.1 // Curva suave para la línea
    },
    {
      label: 'Puntuaciones',
      backgroundColor: '#42b983', // Color de las barras
      data: props.DISC, // Tus 4 números
      type: 'bar'
    }
  ]
});

const chartOptions = {
  responsive: true,
  scales: {
    y: {
      beginAtZero: true
    }
  }
};
</script>

<template>
  <div>
    <div>
        <h1>Perfil DISC</h1>
        <Bar :data="chartData" :options="chartOptions" />

        <div>
          <p>Mis temperamentos predominantes son:</p>
            <h3 v-if="props.DISC[0]>30">Dominante: {{ props.DISC[0] }}</h3>
            <h3 v-if="props.DISC[1]>30">Influyente: {{ props.DISC[1] }}</h3>
            <h3 v-if="props.DISC[2]>30">Solido: {{ props.DISC[2] }}</h3>
            <h3 v-if="props.DISC[3]>30">Concienzudo: {{ props.DISC[3] }}</h3>
        </div>

        <button @click="goBack">Volver a realizar cuestionario</button>
    </div>
    <div>
      <TempD v-if="props.DISC[0]>30" />
      <TempI v-if="props.DISC[1]>30" />
      <TempS v-if="props.DISC[2]>30" />
      <TempC v-if="props.DISC[3]>30" />
    </div>
    
  </div>
</template>

<style scoped>

</style>