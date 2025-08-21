<script setup>
import GroupCaracteristic from './GroupCaracteristic.vue';
const emit = defineEmits(['continue', 'back']);

const goNext = () => {
  emit('continue');
}

const goBack = () => {
  emit('back');
}

</script>

<template>
    <div>
        <h1>Cuestionario</h1>
          <div class="quiz-container">
    
            <GroupCaracteristic v-bind:names="['Enérgico', 'Vivaz', 'Modesto', 'Discreto']" />
            <GroupCaracteristic v-bind:names="['Agresivo', 'Emotivo', 'Complaciente', 'Constante']" />
            <GroupCaracteristic v-bind:names="['Directo', 'Animoso', 'Agradable', 'Acertado']" />


            <GroupCaracteristic v-bind:names="['Directo', 'Animoso', 'Agradable', 'Acertado']" />
            <GroupCaracteristic v-bind:names="['Directo', 'Animoso', 'Agradable', 'Acertado']" />
            <GroupCaracteristic v-bind:names="['Directo', 'Animoso', 'Agradable', 'Acertado']" />
            <GroupCaracteristic v-bind:names="['Directo', 'Animoso', 'Agradable', 'Acertado']" />

        </div>
    </div>

</template>

<style scoped>
.quiz-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    border-radius: 10px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 20px;
}

</style>