<template>
  <div class="carousel-container">
    <h2 class="section-title carousel-title">Nuestro lugar seguro</h2>
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
          <img 
            :src="typeof img === 'string' ? img : img.src" 
            :alt="`Foto ${index + 1}`" 
            class="carousel-image" 
            :style="{ objectPosition: typeof img === 'object' && img.position ? img.position : 'center' }"
          />
        </div>
      </div>

      <button @click="handlePrev" class="nav-btn prev-btn" aria-label="Anterior">
        <ChevronLeftIcon />
      </button>
      <button @click="handleNext" class="nav-btn next-btn" aria-label="Siguiente">
        <ChevronRightIcon />
      </button>

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
      {src: '/images/carousel-1.jpg', position: 'bottom'},
      '/images/carousel-2.jpg',
      { src: '/images/carousel-3.jpg', position: 'top' }, // REVISAR DESPUES SI ES MEJOR CORTAR LA FOTO
      '/images/carousel-4.jpg',
      '/images/carousel-5.jpg',
    ]
  }
});

const currentIndex = ref(0);
let autoPlayInterval = null;

// VER SI DESPUES CONVIENE SACAR EL AUTOPLAY
const startAutoPlay = () => {
  stopAutoPlay();
  autoPlayInterval = setInterval(nextSlide, 6000);
};
const stopAutoPlay = () => {
  if (autoPlayInterval) {
    clearInterval(autoPlayInterval);
    autoPlayInterval = null;
  }
};
const resetAutoPlay = () => {
  startAutoPlay();
};

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % props.images.length;
};
const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + props.images.length) % props.images.length;
};
const handleNext = () => {
  nextSlide();
  resetAutoPlay();
};
const handlePrev = () => {
  prevSlide();
  resetAutoPlay();
};

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
      handleNext();
    } else {
      handlePrev();
    }
  }
};

onMounted(() => {
  startAutoPlay();
});

onUnmounted(() => {
  stopAutoPlay();
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
  line-height: 1.9rem;
  font-weight: 500;
  margin-bottom: 1rem;
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
  top: 90%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.85);
  color: $color-primary;
  border-radius: 50%;
  width: 25px;
  height: 25px;
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
