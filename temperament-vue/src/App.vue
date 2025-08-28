<script setup>
import { ref } from 'vue';
import DescriptionView from './components/DescriptionView.vue';
import InstructionView from './components/InstructionView.vue';
import Quiz from './components/Quiz.vue';
import GraphDISC from './components/GraphDISC.vue';

const currentView= ref('description');

const changeView=(viewName) => {
  currentView.value = viewName;
}

const changeViewGraph = ({ disc }) => {
  // Aquí puedes manejar los datos que vienen del evento
  console.log('Datos recibidos en changeViewGraph:', disc);
  currentView.value = 'graph';
  discData.value=[...disc];
  
};

const discData = ref([0,0,0,0]);

</script>

<template>
  <DescriptionView 
    v-if="currentView === 'description'" 
    @continue="changeView('instruction')"
  />
  <InstructionView 
    v-if="currentView === 'instruction'" 
    @back="changeView('description')"
    @continue="changeView('quiz')"
  />
  <Quiz
    v-if="currentView === 'quiz'"
    @back="changeView('instruction')"
    @continue="changeViewGraph"
  />

  <GraphDISC
    v-if="currentView === 'graph'"
    @back="changeView('quiz')"
    v-bind:DISC="discData"
  />

</template>

<style scoped>

#app {
  max-width: 1400px; /* O un valor mayor que 1200px */
  margin: 0 auto;
  padding: 20px;
}


</style>
