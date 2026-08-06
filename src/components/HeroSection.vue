<template>
  <header class="hero-section">
    <div class="hero-image-wrapper">
      <img :src="coverImage" alt="Nuestra Boda" class="hero-image" />
      <div class="hero-overlay"></div>
      <div class="hero-header-content">
        <p class="pre-title">¡Nos Casamos!</p>
        <h1 class="couple-names">{{ coupleNames }}</h1>
        <p class="hero-message">{{ shortMessage }}</p>
      </div>
    </div>

    <div class="section-container">
      <div class="glass-card date-card">
        <div class="calendar-icon-wrapper">
          <CalendarIcon class="calendar-icon" />
        </div>
        <p class="wedding-date-text">{{ formattedDate }}</p>
        <p class="wedding-time-text">{{ weddingTime }} hs</p>
        
        <div class="action-buttons">
          <a :href="googleCalendarUrl" target="_blank" rel="noopener" class="btn-secondary">
            <CalendarPlusIcon /> Agendar Fecha
          </a>
          <a :href="rsvpFormUrl" target="_blank" rel="noopener" class="btn-primary">
            <CheckCircleIcon /> Confirmar Asistencia
          </a>
        </div>

        <CountdownTimer :targetDate="weddingIsoDate" />
      </div>
    </div>
  </header>
</template>

<script setup>
import { computed } from 'vue';
import { Calendar as CalendarIcon, CalendarPlus as CalendarPlusIcon, CheckCircle as CheckCircleIcon } from '@lucide/vue';
import CountdownTimer from './CountdownTimer.vue';

const props = defineProps({
  coupleNames: {
    type: String,
    default: 'Nombre 1 & Nombre 2'
  },
  shortMessage: {
    type: String,
    default: 'Queremos compartir con vos este momento tan especial en nuestras vidas.'
  },
  coverImage: {
    type: String,
    default: '/images/hero-cover.png'
  },
  weddingDateStr: {
    type: String,
    default: 'Sábado, 21 de Noviembre de 2026'
  },
  weddingTime: {
    type: String,
    default: '18:00'
  },
  weddingIsoDate: {
    type: String,
    default: '2026-11-21T18:00:00'
  },
  rsvpFormUrl: {
    type: String,
    default: 'https://forms.google.com'
  }
});

const formattedDate = computed(() => props.weddingDateStr);

const googleCalendarUrl = computed(() => {
  const title = encodeURIComponent(`Boda ${props.coupleNames}`);
  const details = encodeURIComponent('¡Te esperamos para celebrar nuestra boda!');
  const location = encodeURIComponent('Salón de Fiestas');
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
  background: linear-gradient(to bottom, rgba(0,0,0,0.15) 0%, rgba(0,0,0,0.7) 100%);
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

.pre-title {
  font-family: $font-title;
  font-size: 1.3rem;
  font-style: italic;
  letter-spacing: 2px;
  margin-bottom: 0.3rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.6rem;
    margin-bottom: 0.5rem;
  }
}

.couple-names {
  font-size: 2.6rem;
  line-height: 1.15;
  margin-bottom: 0.8rem;
  text-shadow: 0 4px 15px rgba(0,0,0,0.35);

  @media (min-width: $breakpoint-tablet) {
    font-size: 3.8rem;
    margin-bottom: 1rem;
  }
}

.hero-message {
  font-size: 0.95rem;
  font-weight: 300;
  opacity: 0.95;
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.5;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.1rem;
  }
}

.date-card {
  margin-top: -2.8rem;
  position: relative;
  z-index: 3;

  @media (min-width: $breakpoint-tablet) {
    margin-top: -4rem;
  }
}

.calendar-icon-wrapper {
  width: 52px;
  height: 52px;
  background: rgba(184, 147, 85, 0.1);
  color: $color-primary;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 0.8rem auto;

  @media (min-width: $breakpoint-tablet) {
    width: 60px;
    height: 60px;
    margin-bottom: 1rem;
  }

  .calendar-icon {
    width: 24px;
    height: 24px;

    @media (min-width: $breakpoint-tablet) {
      width: 28px;
      height: 28px;
    }
  }
}

.wedding-date-text {
  font-family: $font-title;
  font-size: 1.5rem;
  color: $color-text;
  font-weight: 700;

  @media (min-width: $breakpoint-tablet) {
    font-size: 2rem;
  }
}

.wedding-time-text {
  font-size: 1rem;
  color: $color-primary;
  font-weight: 600;
  margin-bottom: 1.2rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.1rem;
    margin-bottom: 1.5rem;
  }
}

.action-buttons {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  margin-bottom: 1.5rem;

  @media (min-width: $breakpoint-tablet) {
    flex-direction: row;
    gap: 1rem;
  }
}
</style>
