<script setup>
import { ref } from 'vue';
import CompCaracteristic from './CompCaracteristic.vue';

const traits = ref([
  { id: 1, text: 'Trait 1', initialValue: 2 },
  { id: 2, text: 'Trait 2', initialValue: 3 },
  { id: 3, text: 'Trait 3', initialValue: 1 },
]);

const updateTraitValue = (id, text, value) => {
  console.log(`Updated ${text} (ID: ${id}) to ${value}`);
};
</script>

<template>
    <div>
        <CompCaracteristic
          v-for="trait in traits"
          :key="trait.id"
          :trait-text="trait.text"
          :trait-id="trait.id"
          :initial-value="trait.initialValue"
          @update-value="updateTraitValue"
        />
    </div>
</template>

<style scoped>

</style>