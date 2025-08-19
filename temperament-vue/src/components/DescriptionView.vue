<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['continue']);

const goNext = () => {
  emit('continue');
}

</script>

<template>
  <div class="container">
    <h1>Determinacíon del Temperamento</h1>
    <div class="statement-wrapper">
      <div class="text-content">
        <p>
          Temperamento es la fuerza que impulsa a una persona y refleja ciertas características de ella.
          <br />
          En algunas personas predomina la ira como fuerza impulsadora y en otras el temor. En cualquier caso, los extremos pueden ser inconvenientes.
        </p>
        <p>
          Ningún temperamento es mejor que otro, simplemente somos diferentes; en la vida real, los proyectos exitosos requieren personas de diferentes temperamentos.Los enunciados que dicen: "Muestra Ira, pero no peques" y "No descartes las cosas por que sean peligrosas", muestran un principio importante: cuando mas peligrosas sean lass energías, mayor será su valorsi las podemos controlar.
        </p>
      </div>
      <div class="image-content">
        <h2>Temperamento</h2>
        <img src="/Temperament1.webp" alt="Temperamento" class="image-responsive" />
      </div>
    </div>
    <button @click="goNext">Continuar</button>
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
  line-height: 1.4rem; /* Mejora la legibilidad del texto */
  font-size: 2rem; /* Tamaño de fuente base */
}

/* Estilo para la imagen reactiva */
.responsive-image {
  max-width: 80%; /* Asegura que la imagen no sobrepase el ancho de su contenedor */
  height: auto; /* Mantiene la proporción de la imagen */
}

/*--------------------------------------------------------------------------------------------------------------------*/

/* Estilos para pantallas de computadora (más de 768px de ancho) */
@media (min-width: 768px) {
  .statement-wrapper {
    flex-direction: row; /* En pantallas grandes, coloca los elementos en una fila */
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
