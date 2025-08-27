<script setup>
import { ref } from 'vue';
import GroupCaracteristic from './GroupCaracteristic.vue';
const emit = defineEmits(['continue', 'back']);

const goNext = () => {
  emit('continue');
}

const goBack = () => {
  emit('back');
}

const question= ref(0)

const Totales = ref([0,0,0,0])
const Sumas = ref([0,0,0,0])

const enableNextQuestion = ref(false);
const enableResult = ref(false);


const handleUpdate = ({ values, enable }) => {
  console.log('Valores en el padre:', values);
  console.log('Enable en el padre:', enable);
  enableNextQuestion.value = enable;
  if (enable) {
    Sumas.value = values;
    console.log('Sumas actualizadas:', Sumas.value);
  }
};

const goNextQuestion = () => {
  Totales.value = Totales.value.map((total, index) => total + Sumas.value[index]);
  console.log('Totales actualizados:', Totales.value);
  enableNextQuestion.value = false;
  question.value++;
  if (question.value > 10) {
    enableResult.value = true;
  }
}

</script>

<template>
    <div class="container">
        <div class="header">
          <h1>Cuestionario</h1>
          <h2>temperamento</h2>
        </div>
        <div class="quiz-container">

            <GroupCaracteristic
              v-if="question === 0"
              v-bind:names="['Enérgico', 'Vivaz', 'Modesto', 'Discreto']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 1"
              v-bind:names="['Agresivo', 'Emotivo', 'Complaciente', 'Constante']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 2"
              v-bind:names="['Directo', 'Animoso', 'Agradable', 'Acertado']"
              @update="handleUpdate"
            />


        </div>
        <div class="button-container">
            <button @click="goBack">Atras</button>
            <button @click="goNextQuestion" :disabled="!enableNextQuestion && question<=10" >Siguiente Pregunta</button>
            <button @click="goResult" :disabled="!enableResult">Resultados</button>
        </div>
    </div>
</template>

<style scoped>

/* Estilos para el contenedor principal */
.container {
  max-width: 1200px;
  margin: 0 auto; /* Centra el contenedor en la página */
  padding: 20px;
  text-align: center;
}

.button-container {
  display: flex;
  justify-content: space-between; /* Distribuye los botones a los extremos */
  margin-top: 20px; /* Espacio entre el contenido y los botones */
}

.quiz-container {
    max-width: 1200%;
    margin: 0 auto;
    padding: 20px;
    border-radius: 10px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 20px;
}

@media (min-width: 768px) {
  .statement-wrapper {
    flex-direction: column; /* En pantallas grandes, coloca los elementos en una fila */
    justify-content: space-between; /* Distribuye el espacio entre los elementos */
    align-items: flex-start; /* Alinea los elementos en la parte superior */
  }

}


</style>