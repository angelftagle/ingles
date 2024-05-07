<template>
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <div class="swiper-slide" v-for="(item, index) in items" :key="index">
        <!-- Contenido de cada slide del carrusel -->
        <img :src="item.image" alt="Slide" />
      </div>
    </div>
    <!-- Agrega paginación y botones de navegación -->
    <div class="swiper-pagination"></div>
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
  </div>
</template>

<script>
import 'swiper/swiper-bundle.css'; // Importa los estilos de Swiper
import { Swiper, SwiperSlide } from 'vue-awesome-swiper';

export default {
  components: {
    Swiper,
    SwiperSlide
  },
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  // Configura Swiper
  data() {
    return {
      swiperOptions: {
        loop: true,
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      }
    };
  }
};
</script>

<style scoped>
/* Estilos específicos para el carrusel */
.swiper-container {
  width: 100%;
  height: 100%;
}

.swiper-slide img {
  width: 100%;
  height: 100%;
}
</style>
