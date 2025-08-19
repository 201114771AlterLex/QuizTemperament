<script setup>
import { defineEmits } from 'vue';
import CompCaracteristic from './CompCaracteristic.vue';

const emit = defineEmits(['continue', 'back']);

const goNext = () => {
  emit('continue');
}

const goBack = () => {
  emit('back');
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
          <li>Califica las palabras, de cada fila horizontal, en una escala de 1 a 4. La calificación dada, debe indicar qué tanto te describe cada palabra, asignando <b>4</b> a la que más te describe de todas ellas y <b>1</b> a la que menos</li>
          <li>En una línea horizontal no puede haber dos palabras con la misma calificación. A continuación aparece un ejemplo</li>
        </ul>
        
      </div>
      <div>
        <h2>Ejemplo</h2>
        <CompCaracteristic traitText="Amable" traitId="1" />
        <CompCaracteristic traitText="Sincero" traitId="2" />
        <CompCaracteristic traitText="Tierno" traitId="3" />
        <CompCaracteristic traitText="Sociable" traitId="4" />
      </div>
    </div>

    <button @click="goBack">Atras</button>
    <button @click="goNext">Comenzar Cuestionario</button>
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
.text-content p li {
  line-height: 1.3rem; /* Mejora la legibilidad del texto */
  font-size: 1.4rem; /* Tamaño de fuente base */
}

/*--------------------------------------------------------------------------------------------------------------------*/

/* Estilos para pantallas de computadora (más de 768px de ancho) */
@media (min-width: 768px) {
  .statement-wrapper {
    flex-direction: column; /* En pantallas grandes, coloca los elementos en una fila */
    justify-content: space-between; /* Distribuye el espacio entre los elementos */
    align-items: flex-start; /* Alinea los elementos en la parte superior */
  }

  .text-content, .image-content {
    flex: 1; /* Otorga un ancho flexible a ambos contenedores */
  }

  /* Ajusta el tamaño de la fuente para que el texto sea más grande en computadoras */
  .text-content p {
    font-size: 1.6rem;
  }
}
</style>