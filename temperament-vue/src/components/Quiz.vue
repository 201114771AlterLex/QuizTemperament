<script setup>
import { ref , computed } from 'vue';
import GroupCaracteristic from './GroupCaracteristic.vue';
const emit = defineEmits(['continue', 'back']);

const goGraph = () => {
  emit('continue', {disc: Totales.value});
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
  //console.log('Valores en el padre mandados del hijo:', values);
  //console.log('Enable en el padre mandados del hijo:', enable);
  enableNextQuestion.value = enable;
  if (enable) {
    Sumas.value = [...values];
    //console.log('Sumas actualizadas temporales para sumar a totales:', Sumas.value);
  }
  else{
    Sumas.value = [0,0,0,0];
    //console.log('Sumas actualizadas reseteadas:', Sumas.value);
  }
};

const goNextQuestion = () => {
  //console.log('Pregunta actual:', question.value);
  if (question.value <= 11){
    Totales.value = Totales.value.map((total, index) => total + Sumas.value[index]);
    //console.log('Totales actualizados:', Totales.value);
    enableNextQuestion.value = false;
    question.value++;
  }
  if (question.value > 11) {
    enableNextQuestion.value = false; 
    enableResult.value = true;
  }
};

const buttonText = computed(() => {
  if (question.value < 11) {
    return 'Siguiente Pregunta';
  } else {
    return 'Ver puntuaciones';
  }
});

</script>

<template>
    <div class="container">
        <div class="header">
          <h1>Cuestionario</h1>
          <h2>Temperamento</h2>
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

            <GroupCaracteristic
              v-if="question === 3"
              v-bind:names="['Tenaz', 'Compasivo', 'Dócil', 'Perfeccionista']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 4"
              v-bind:names="['Atrevido', 'Impulsivo', 'Amable', 'Precavido']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 5"
              v-bind:names="['Competitivo', 'Expresivo', 'Sustentador', 'Preciso']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 6"
              v-bind:names="['Arriesgado', 'Hablador', 'Relajado', 'Objetivo']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 7"
              v-bind:names="['Argumentador', 'Divertido', 'Paciente', 'Lógico']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 8"
              v-bind:names="['Audaz', 'Espontáneo', 'Estable', 'Organizado']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 9"
              v-bind:names="['Dirigente', 'Optimista', 'Apacible', 'Concienzudo']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 10"
              v-bind:names="['Decidido', 'Alegre', 'Leal', 'Serio']"
              @update="handleUpdate"
            />

            <GroupCaracteristic
              v-if="question === 11"
              v-bind:names="['Independiente', 'Entusiasta', 'Buen oyente', 'Altas Normas']"
              @update="handleUpdate"
            />

            <div v-if="question === 12">
              <table>
                <thead>
                  <tr>
                    <th> </th>
                    <th>D</th>
                    <th>I</th>
                    <th>S</th>
                    <th>C</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>Puntuaciones</td>
                    <td>{{ Totales[0] }}</td>
                    <td>{{ Totales[1] }}</td>
                    <td>{{ Totales[2] }}</td>
                    <td>{{ Totales[3] }}</td>
                  </tr>
                </tbody>
              </table>
            </div>

        </div>
        <div class="button-container">
            <button @click="goBack">Atras</button>
            <button @click="goNextQuestion" :disabled="!enableNextQuestion" >{{ buttonText }}</button>
            <button @click="goGraph" :disabled="!enableResult">Grafica</button>
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
  .container{
    width: 25rem;
  }

}

/* Estilos específicos para la tabla de puntuaciones */
table {
  width: 100%; /* La tabla ocupa todo el ancho disponible */
  border-collapse: collapse; /* Elimina los espacios entre los bordes de las celdas */
  margin: 20px 0; /* Espacio arriba y abajo para separarla de otros elementos */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Sombra sutil para un efecto de elevación */
  border-radius: 8px; /* Bordes redondeados */
  overflow: hidden; /* Asegura que los bordes redondeados se apliquen a todo el contenido */
  background-color: #fff; /* Fondo blanco para la tabla */
  font-family: Arial, sans-serif; /* Fuente legible */
  font-size: 1.1em;
}

/* Estilos para el encabezado de la tabla */
thead {
  background-color: #b1b8de; /* Fondo gris claro para el encabezado */
}

/* Estilos para las celdas del encabezado (<th>) */
th {
  padding: 12px 15px; /* Espaciado interno */
  text-align: center; /* Centra el texto */
  font-weight: bold; /* Texto en negrita */
  color: #333; /* Color de texto oscuro */
  border-bottom: 2px solid #ddd; /* Línea en la parte inferior de la celda */
  font-size: 1.2em;
}

/* Estilos para las filas de la tabla */
tbody tr {
  border-bottom: 1px solid #eee; /* Línea sutil entre filas */
  transition: background-color 0.3s ease; /* Transición suave al pasar el mouse */
}

/* Efecto al pasar el cursor sobre las filas */
tbody tr:hover {
  background-color: #f9f9f9; /* Fondo más claro al pasar el mouse */
}

/* Estilos para las celdas del cuerpo (<td>) */
td {
  padding: 12px 15px; /* Espaciado interno */
  text-align: center; /* Centra el texto */
  color: #555; /* Color de texto gris */
  font-size: 1.1em;
}

/* Estilos para la primera celda de la fila (la etiqueta 'Puntuaciones') */
td:first-child {
  font-weight: bold; /* Pone 'Puntuaciones' en negrita */
}


</style>