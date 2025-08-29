
<script setup>
import { ref } from 'vue';

// Array de objetos para las tarjetas
const cards = ref([
    {
        title: 'PAUTAS PARA LA SUPERACIÓN',
        content: 'Ponerse objetivos altos y fijarse un tiempo para alcanzarlos. Fortalecer su voluntad desarrollando hábitos que le permitan vencer su pasividad y conformidad: Involucrarse en grupos que le ayuden al servicio de los demás, balancear su mente con su corazón cálido. Escuchar con apertura de lo que los demás dicen, sacando provecho de todo lo positivo. Decir lo que siente y demostrar con detalle su afecto.',
    },
    {
        title: 'Cualidades',
        content: 'Es tranquilo, sereno, alegre, se lleva personalmente bien con los demás. Es eficiente, conservador, confiable e ingenioso, con una mentalidad definidamente práctica. Es cortés en todo tipo de tarea o responsabilida. Se desarrolla sustentando y cooperando con otros. Se desenvuelve mejor en medios armoniosos y de apoyo. Los flemáticos, son buenos maestros, médicos, científicos, comediantes y editores de libros.',
    },
    {
        title: 'Debilidades',
        content: 'Falta de motivación, ve la vida como si fuera un espectador para evitar "verse envuelto". Tiende a ser terco, mezquino, no revela sus sentimientos, es indeciso. Detesta los cambios y no se enfrenta.',
    },
]);

// Índice de la tarjeta actual, comienza en 0
const currentCardIndex = ref(0);

// Función para ir a la tarjeta anterior
const prevCard = () => {
  if (currentCardIndex.value > 0) {
    currentCardIndex.value--;
  }
};

// Función para ir a la tarjeta siguiente
const nextCard = () => {
  if (currentCardIndex.value < cards.value.length - 1) {
    currentCardIndex.value++;
  }
};
</script>

<template>
    <div id="tempD">
        <h1>Sólido / Flemático</h1>
        <div id="notc">

            <p> <u><b>Necesidad:</b></u> de estabilidad</p>
            <p> <u><b>Orientación:</b></u> a procesos</p>
            <p> <u><b>Temor:</b></u> perder estabilidad</p>
            <p> <u><b>Comunicación:</b></u> indirecta, recibe información</p>
        </div>
       
        <div id="card-container">
        <div v-for="(card, index) in cards" :key="index" v-show="index === currentCardIndex" class="card">
            <h2>{{ card.title }}</h2>
            <p>{{ card.content }}</p>
        </div>

        <div class="navigation">
            <button @click="prevCard" :disabled="currentCardIndex === 0">Anterior</button>
            <button @click="nextCard" :disabled="currentCardIndex === cards.length - 1">Siguiente</button>
        </div>
        </div>

    </div>




</template>

<style scoped>

/* Estilos para el contenedor principal */
.tempD {
  max-width: 800px;
  margin: 0 auto; /* Centra el contenedor en la página */
  padding: 20px;
  text-align: center;
}

/* Estilos para el título principal */
h1 {
  font-size: 2.5rem; /* Tamaño de fuente para el título */
  margin-bottom: 10px;
}

/* Estilo para el párrafo */
#notc p {
  line-height: 1rem; /* Mejora la legibilidad del texto */
  font-size: 1.1rem; /* Tamaño de fuente base */
}

#notc {
    text-align: left;
    max-width: 800px;
    margin-top: 20px;
    padding: 20px 20px 5px 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

#card-container {
    max-width: 800px;
    margin: 10px auto;
    padding: 5px 20px 5px 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: left;
}

.card {
  padding: 10px 20px;
}

.navigation {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #354455;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:disabled {
  background-color: #1a1f34;
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  background-color: #0056b3;
}

h2 {
  font-size: 1.8rem;
  margin-bottom: 15px;
  border-bottom: 2px solid #007BFF;
  padding-bottom: 5px;
}

/*--------------------------------------------------------------------------------------------------------------------*/

/* Estilos para pantallas de computadora (más de 768px de ancho) */
@media (min-width: 768px) {

  h1 {
  font-size: 3rem; /* Tamaño de fuente para el título */
  margin-bottom: 20px;
}

  #notc {
    max-width: 800px;
    margin: 0 auto;
    flex: 1; /* Otorga un ancho flexible a ambos contenedores */
  }

  /* Ajusta el tamaño de la fuente para que el texto sea más grande en computadoras */
  #notc p {
    font-size: 1.3rem;
  }
}

</style>