<script setup>
import CompCaracteristic from './CompCaracteristic.vue';

const emit = defineEmits(['continue', 'back']);

const goNext = () => {
  emit('continue');
}

const goBack = () => {
  emit('back');
}

const updateValueinsttt = (traitId, traitText, value) => {
  console.log('Valor actualizado:', traitId, traitText, value);
}

</script>

<template>
  <div class="container">
    <h1 id="title">Tendencias DISC</h1>
    <h2 id="subTitle">Determinación del Temperamento</h2>
    <div class="statement-wrapper">
      <div class="text-content">
        <p>
          El ejercicio que vas a realizar, dará una pauta sobre tu temperamento. Para conocer más a fondo sobre el temperamento, se ncesitan estudios mas detallados. Esto es sólo una tendencia.
        </p>
        <h3>Observación importante:</h3>
        <p>
          Consigna en esta evaluación la primera impresión que tienes de ti frente a cada palabra. No hay respuestas buenas ni malas.
        </p>
        <h3>Instrucciones:</h3>       
         <ul>
          <li>Califica las palabras, en una escala de 1 a 4. La calificación dada, debe indicar qué tanto te describe cada palabra, asignando <b>4</b> a la que más te describe de todas ellas y <b>1</b> a la que menos</li>
          <li>En un grupo de cuatro palabras, no puede haber dos palabras con la misma calificación. A continuación aparece ejemplos de correcto e incorrecto</li>
        </ul>
        
      </div>
      <div class="examples">
        <div class="example-container">
          <h2>Ejemplo Correcto</h2>
          <div>
            <CompCaracteristic traitText="Audaz" v-bind:traitId="1" v-bind:disable="true" v-bind:initialValue="2"/>
            <CompCaracteristic traitText="Espontáneo" v-bind:traitId="2" v-bind:disable="true" v-bind:initialValue="1"/>
            <CompCaracteristic traitText="Estable" v-bind:traitId="3" v-bind:disable="true" v-bind:initialValue="4"/>
            <CompCaracteristic traitText="Organizado" v-bind:traitId="4" v-bind:disable="true" v-bind:initialValue="3"/>
          </div>
        </div>

        <div class="example-container">
          <h2>Ejemplo Incorrecto</h2>
          <div>
            <CompCaracteristic traitText="Audaz" v-bind:traitId="1" v-bind:disable="true" v-bind:initialValue="2"/>
            <CompCaracteristic traitText="Espontáneo" v-bind:traitId="2" v-bind:disable="true" v-bind:initialValue="2"/>
            <CompCaracteristic traitText="Estable" v-bind:traitId="3" v-bind:disable="true" v-bind:initialValue="4"/>
            <CompCaracteristic traitText="Organizado" v-bind:traitId="4" v-bind:disable="true" v-bind:initialValue="3"/>
          </div>
        </div>
      </div>
    </div>

    <div class="button-container">
      <button @click="goBack">Atras</button>
      <button @click="goNext">Comenzar Cuestionario</button>
    </div>
    
  </div>
</template>

<style scoped>
#subTitle {
    margin-top: 0;
}
#title{
    margin-bottom: 5px;
}
h3 {
    text-align: left;
    font-weight: bold;
    margin-left: 1rem;
}
/* Estilos para el contenedor principal */
.container {
  max-width: 1200px;
  margin: 0 auto; /* Centra el contenedor en la página */
  padding: 20px;
  text-align: center;
}

/* Estilos para el título principal */
h1 {
  font-size: 3.5rem; /* Tamaño de fuente para el título */
  margin-bottom: 20px;
}


/* Contenedor principal del texto e imagen */
.statement-wrapper {
  display: flex;
  flex-direction: column; /* Por defecto, apila los elementos verticalmente (para móviles) */
  align-items: center;
  gap: 20px; /* Espacio entre el texto y la imagen */
}

/* Contenedor del texto */
.text-content {
  text-align:  justify;
}

/* Estilo para el párrafo */
.text-content p {
  line-height: 1.8rem; /* Mejora la legibilidad del texto */
  font-size: 1.4rem; /* Tamaño de fuente base */
}

.text-content ul {
  font-size: 1.2rem;
}

.example-container {
  margin: 0 auto;
  border: 10px solid #ccc;
  border-radius: 3rem;
  padding: 2rem;
}

.button-container {
  display: flex;
  justify-content: space-around; /* Distribuye los botones a los extremos */
  margin-top: 20px; /* Espacio entre el contenido y los botones */
}

.examples{
  display: flex;
  flex-direction: row;
  gap: 1rem;
  margin: 0 auto;
}

/*--------------------------------------------------------------------------------------------------------------------*/

/* Estilos para pantallas de computadora (más de 768px de ancho) */
@media (min-width: 768px) {
  .statement-wrapper {
    flex-direction: column; /* En pantallas grandes, coloca los elementos en una fila */
    justify-content: space-between; /* Distribuye el espacio entre los elementos */
    align-items: flex-start; /* Alinea los elementos en la parte superior */
  }


  /* Ajusta el tamaño de la fuente para que el texto sea más grande en computadoras */
.text-content p ul{
    font-size: 1.6rem;
  }

.text-content ul {
  font-size: 1.4rem;
}

}
</style>