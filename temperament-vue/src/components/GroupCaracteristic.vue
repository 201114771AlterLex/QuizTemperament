<script setup>
import { ref, watch } from 'vue';
import CompCaracteristic from './CompCaracteristic.vue';

const props = defineProps({
  names: {
    type: Array,
    default: () => [],
  },
  values: {
    type: Array,
    default: () => [0, 0, 0, 0]
  },
  enable: {
    type: Boolean,
    default: false
  },
});

const emit = defineEmits(['update']);

const localValues = ref([...props.values]);
const localEnable = ref(props.enable);

const updateTraitValue = (id, text, value) => {
  //console.log(`Updated ${text} (ID: ${id}) to ${value}`);
  localValues.value[id - 1] = value;
  localEnable.value = !localValues.value.includes(0);
  //console.log('Enable status:', localEnable.value);
  //console.log('Props values updated:', localValues.value);
  //console.log('Current group values:', props.names);
  //console.log('Local enable status:', localEnable.value);
  validate();
};

const validate =()=> {
  if (!localEnable.value) {
    return;
  }
  let temp=[1,2,3,4]
  let cpValues = [...localValues.value];
  console.log('Final before delete values:', cpValues);
  for (let index = 0; index < temp.length; index++) {
    let indexx=cpValues.indexOf(temp[index])
    if (indexx !== -1) {
      cpValues.splice(indexx, 1);
    }
  }
  console.log('Final values:', cpValues);
  console.log(cpValues.length);
  if (cpValues.length === 0) {
    console.log('All values are unique. Proceeding to save:', localValues.value);
    // Aquí puedes emitir un evento o llamar a una función para guardar los valores
    emit('update', {
    values: localValues.value,
    enable: localEnable.value
  });
  } else {
    console.log('There are duplicate values. Please ensure all values are unique.');
    emit('update', {
      values: localValues.value,
      enable: false,
    });
  }
}


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