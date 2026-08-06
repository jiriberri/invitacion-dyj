<template>
  <div class="carousel-container">
    <h2 class="carousel-title">Nuestros Momentos</h2>
    <div class="carousel-slider">
      <div 
        class="carousel-track" 
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
      >
        <div 
          v-for="(img, index) in images" 
          :key="index" 
          class="carousel-slide"
        >
          <img :src="img" :alt="`Foto ${index + 1}`" class="carousel-image" />
        </div>
      </div>

      <button @click="prevSlide" class="nav-btn prev-btn" aria-label="Anterior">
        <ChevronLeftIcon />
      </button>
      <button @click="nextSlide" class="nav-btn next-btn" aria-label="Siguiente">
        <ChevronRightIcon />
      </button>
    </div>

    <!-- Indicadores / Puntos -->
    <div class="indicators">
      <span 
        v-for="(img, index) in images" 
        :key="index"
        :class="['dot', { active: currentIndex === index }]"
        @click="currentIndex = index"
      ></span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { ChevronLeft as ChevronLeftIcon, ChevronRight as ChevronRightIcon } from '@lucide/vue';

const props = defineProps({
  images: {
    type: Array,
    default: () => [
      '/images/carousel-1.png',
      '/images/carousel-2.png',
      '/images/hero-cover.png'
    ]
  }
});

const currentIndex = ref(0);
let autoPlayInterval = null;

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % props.images.length;
};

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + props.images.length) % props.images.length;
};

onMounted(() => {
  autoPlayInterval = setInterval(nextSlide, 4500);
});

onUnmounted(() => {
  if (autoPlayInterval) clearInterval(autoPlayInterval);
});
</script>

<style lang="scss" scoped>
.carousel-container {
  width: 100%;
  max-width: 850px;
  margin: 3rem auto;
  padding: 0 1rem;
  text-align: center;
}

.carousel-title {
  font-family: $font-title;
  font-size: 2.2rem;
  color: $color-primary;
  margin-bottom: 1.5rem;
}

.carousel-slider {
  position: relative;
  width: 100%;
  height: 450px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: $shadow-card;

  @media (max-width: $breakpoint-tablet) {
    height: 300px;
  }
}

.carousel-track {
  display: flex;
  width: 100%;
  height: 100%;
  transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
}

.carousel-slide {
  min-width: 100%;
  height: 100%;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.85);
  color: $color-primary;
  border-radius: 50%;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(0,0,0,0.15);
  transition: $transition-smooth;
  z-index: 5;

  &:hover {
    background: $color-white;
    transform: translateY(-50%) scale(1.1);
  }

  &.prev-btn {
    left: 1rem;
  }

  &.next-btn {
    right: 1rem;
  }
}

.indicators {
  display: flex;
  justify-content: center;
  gap: 0.6rem;
  margin-top: 1rem;

  .dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: $color-border;
    cursor: pointer;
    transition: $transition-smooth;

    &.active {
      background: $color-primary;
      width: 24px;
      border-radius: 12px;
    }
  }
}
</style>
