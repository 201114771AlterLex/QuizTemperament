<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({
  traitText: String,
  traitId: Number,
  disable: {
    type: Boolean,
    default: false
  },
  initialValue: {
    type: Number,
    default: null
  }
});

const emit = defineEmits(['update-value']);

const selectedValue = ref(props.initialValue);

const selectValue = (value) => {
  selectedValue.value = value;
  emit('update-value', props.traitId, props.traitText, value);
};
</script>

<template>
  <div class="trait-item">
    <div class="selection-box">
      <div 
        class="option" 
        :class="{ 'selected': selectedValue === 1 }" 
        @click="selectValue(1)">
        1
      </div>
      <div 
        class="option" 
        :class="{ 'selected': selectedValue === 2 }" 
        @click="selectValue(2)">
        2
      </div>
      <div 
        class="option" 
        :class="{ 'selected': selectedValue === 3 }" 
        @click="selectValue(3)">
        3
      </div>
      <div 
        class="option" 
        :class="{ 'selected': selectedValue === 4 }" 
        @click="selectValue(4)">
        4
      </div>
    </div>
    <span class="trait-text">{{ traitText }}</span>
  </div>
</template>

<style scoped>
.trait-item {
  display: flex;
  align-items: center;
  gap: 15px;
}

.selection-box {
  display: flex;
  border: 1px solid #ccc;
  grid-template-columns: repeat(2, 1fr);
  border-radius: 5px;
  overflow: hidden;
}

.option {
  /* Tamaño del cuadro */
  width: 30px; 
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  user-select: none;
  border-right: 1px solid #ccc;
  transition: background-color 0.2s ease;
  font-weight: bold;
}

.option:last-child {
  border-right: none;
}

.option.selected {
  background-color: #3e73d3; /* Color de fondo para la selección */
  color: white; /* Color de texto para la selección */
  border-color: #3e73d3;
}

.option:hover:not(.selected) {
  background-color: #e0e0e0;
}

.trait-text {
  font-size: 1.1em;
  white-space: nowrap; /* Evita que el texto se parta en varias líneas */
}

.trait-item.disabled {
  /* Estilos para el contenedor cuando está deshabilitado */
  opacity: 0.6;
  cursor: not-allowed;
}
.option.disabled-option {
  cursor: not-allowed;
  /* Opcional: Desactiva el hover */
  pointer-events: none;
}

</style>