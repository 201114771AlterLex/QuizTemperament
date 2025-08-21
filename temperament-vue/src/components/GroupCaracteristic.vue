<script setup>
import { ref } from 'vue';
import CompCaracteristic from './CompCaracteristic.vue';

const props = defineProps({
  names: {
    type: Array,
    default: () => [],
  },
  values: {
    type: Array,
    default: () => []
  }
});


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
    <div class="group-container">
        <CompCaracteristic
          v-for="n in 4"
          :key="n"
          :trait-text="props.names[n - 1]"
          :trait-id="n"
          @update-value="updateTraitValue"
        />
        <br>
        <button>Guardar</button>
    </div>
</template>

<style scoped>
.group-container {
  margin: 0 auto;
  border: 10px solid #ccc;
  border-radius: 3rem;
  padding: 2rem;
}
</style>