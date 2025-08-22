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

const handleUpdate = ({ values, enable }) => {
  console.log('Valores en el padre:', values);
  console.log('Enable en el padre:', enable);
};

const goNextQuestion = () => {
  question.value++;
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


        </div>
        <div class="button-container">
            <button @click="goBack">Atras</button>
            <button @click="goNext">Siguiente Pregunta</button>
            <button @click="goNextQuestion">Siguiente Pregunta</button>
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