<template>
  <div class="carousel-container">
    <h2 class="carousel-title">Nuestros Momentos</h2>
    <div 
      class="carousel-slider"
      @touchstart="onTouchStart"
      @touchend="onTouchEnd"
    >
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

// Gestos táctiles para dispositivos móviles
let touchStartX = 0;

const onTouchStart = (e) => {
  touchStartX = e.touches[0].clientX;
};

const onTouchEnd = (e) => {
  const touchEndX = e.changedTouches[0].clientX;
  const diff = touchStartX - touchEndX;
  if (Math.abs(diff) > 40) {
    if (diff > 0) {
      nextSlide();
    } else {
      prevSlide();
    }
  }
};

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
  margin: 2rem auto;
  padding: 0 1rem;
  text-align: center;

  @media (min-width: $breakpoint-tablet) {
    margin: 3.5rem auto;
  }
}

.carousel-title {
  font-family: $font-title;
  font-size: 1.8rem;
  color: $color-primary;
  margin-bottom: 1.2rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 2.2rem;
    margin-bottom: 1.5rem;
  }
}

.carousel-slider {
  position: relative;
  width: 100%;
  height: 280px;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: $shadow-card;
  user-select: none;

  @media (min-width: $breakpoint-tablet) {
    height: 450px;
    border-radius: 24px;
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
  width: 38px;
  height: 38px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  transition: $transition-smooth;
  z-index: 5;

  @media (min-width: $breakpoint-tablet) {
    width: 44px;
    height: 44px;
  }

  &:hover {
    background: $color-white;
    transform: translateY(-50%) scale(1.08);
  }

  &.prev-btn {
    left: 0.6rem;

    @media (min-width: $breakpoint-tablet) {
      left: 1rem;
    }
  }

  &.next-btn {
    right: 0.6rem;

    @media (min-width: $breakpoint-tablet) {
      right: 1rem;
    }
  }
}

.indicators {
  display: flex;
  justify-content: center;
  gap: 0.6rem;
  margin-top: 1rem;

  .dot {
    width: 9px;
    height: 9px;
    border-radius: 50%;
    background: $color-border;
    cursor: pointer;
    transition: $transition-smooth;

    &.active {
      background: $color-primary;
      width: 22px;
      border-radius: 12px;
    }
  }
}
</style>
