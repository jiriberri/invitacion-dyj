<template>
  <header class="hero-section">
    <div class="hero-image-wrapper">
      <img :src="coverImage" alt="Nuestra Boda" class="hero-image" />
      <div class="hero-overlay"></div>
      <div class="hero-header-content">
        <h1 class="couple-names">{{ coupleNames }}</h1>
        <p class="pre-title">¡Nos casamos!</p>
      </div>
    </div>

    <div class="section-container">
      <div class="glass-card date-card">
        <p class="wedding-date-text">{{ formattedDate }}</p>
        
        <p class="until-wedding">FALTAN...</p>
        <CountdownTimer :targetDate="weddingIsoDate" />
        
        <div class="action-buttons">
          <a :href="googleCalendarUrl" target="_blank" rel="noopener" class="btn-secondary">
            <CalendarPlusIcon /> AGENDAR FECHA
          </a>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { computed } from 'vue';
import { CalendarPlus as CalendarPlusIcon } from '@lucide/vue';
import CountdownTimer from './CountdownTimer.vue';

const props = defineProps({
  coupleNames: {
    type: String,
    default: 'Dai & Juli'
  },
  coverImage: {
    type: String,
    default: '/images/hero-cover.jpg'
  },
  weddingDateStr: {
    type: String,
    default: '31 DE OCTUBRE DE 2026'
  },
  weddingTime: {
    type: String,
    default: '21:00'
  },
  weddingIsoDate: {
    type: String,
    default: '2026-10-31T21:00:00'
  }
});

const formattedDate = computed(() => props.weddingDateStr.toUpperCase());

const googleCalendarUrl = computed(() => {
  const title = encodeURIComponent(`Boda ${props.coupleNames}`);
  const details = encodeURIComponent('¡Te esperamos para celebrar nuestra boda!');
  const location = encodeURIComponent('Salón Ohana Eventos');
  const isoStart = props.weddingIsoDate.replace(/[-:]/g, '');
  return `https://calendar.google.com/calendar/render?action=TEMPLATE&text=${title}&details=${details}&location=${location}&dates=${isoStart}/${isoStart}`;
});
</script>

<style lang="scss" scoped>
.hero-section {
  width: 100%;
}

.hero-image-wrapper {
  position: relative;
  width: 100%;
  height: 65vh;
  min-height: 420px;
  max-height: 750px;
  overflow: hidden;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  text-align: center;

  @media (min-width: $breakpoint-tablet) {
    height: 80vh;
    min-height: 500px;
  }
}

.hero-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, rgba(0,0,0,0.1) 0%, rgba(0,0,0,0.65) 100%);
}

.hero-header-content {
  position: relative;
  z-index: 2;
  color: $color-white;
  padding: 2.5rem 1rem;
  max-width: 800px;

  @media (min-width: $breakpoint-tablet) {
    padding: 3rem 1.5rem;
  }
}

.couple-names {
  font-family: $font-against;
  font-size: 3.5rem;
  font-weight: 400;
  line-height: 6rem;
  color: $color-white;
  text-shadow: 0 4px 15px rgba(0,0,0,0.4);

  @media (min-width: $breakpoint-tablet) {
    font-size: 4rem;
  }
}

.pre-title {
  font-family: $font-title;
  font-size: 1.5rem;
  font-weight: 700;
  color: $color-white;
  margin-bottom: 0.5rem;
  letter-spacing: 0.5px;
  line-height: 3rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.6rem;
  }
}

.date-card {
  margin-top: -2.8rem;
  position: relative;
  z-index: 3;
  background-color: $color-card-bg;

  @media (min-width: $breakpoint-tablet) {
    margin-top: -4rem;
  }
}

.wedding-date-text {
  font-family: $font-title;
  font-size: 1.25rem;
  color: $color-primary;
  font-weight: 700;
  letter-spacing: 1px;
  margin-bottom: 1.2rem;
  line-height: 3rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.6rem;
    margin-bottom: 1.5rem;
  }
}

.until-wedding {
  font-family: $font-tangier;
  font-size: 1rem;
  color: $color-primary;
  font-weight: 400;
  letter-spacing: 1px;

  @media (min-width: $breakpoint-tablet) {
    font-size: 2.2rem;
  }
}

.action-buttons {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  margin-bottom: 1rem;

  @media (min-width: $breakpoint-tablet) {
    flex-direction: row;
    gap: 1rem;
  }
}
</style>
