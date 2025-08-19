<script setup>
import { ref } from 'vue';
import DescriptionView from './components/DescriptionView.vue';
import InstructionView from './components/InstructionView.vue';


const currentView= ref('description');

const changeView=(viewName) => {
  currentView.value = viewName;
}

</script>

<template>
  <DescriptionView 
    v-if="currentView === 'description'" 
    @continue="changeView('instruction')"
  />
  <InstructionView 
    v-if="currentView === 'instruction'" 
    @back="changeView('description')"
    @continue="changeView('questionnaire')"
  />
</template>

<style scoped>

</style>
