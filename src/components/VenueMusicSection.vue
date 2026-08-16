<template>
  <section class="venue-music-section section-container">
    <!-- Ubicación del Salón -->
    <div class="glass-card venue-card">
      <img src="/images/party-logo.gif" alt="Party" class="icon-party">
      <h2 class="section-title">FIESTA</h2>
      <p class="section-subtitle">{{ venueName }}</p>
      <p class="venue-address">{{ venueAddress }}</p>
      <p class="venue-address">21:00 hs</p>
      <p class="venue-time">La ceremonia comienza {{ partyTime }}hs.</p>
      <p class="venue-time venue-disclaimer">¡Sean puntuales!</p>
      
      <div class="action-buttons">
          <a :href="googleMapsUrl" target="_blank" rel="noopener" class="btn-primary">CÓMO LLEGAR</a>
        </div>
    </div>

    <!-- Sugerencia de Música -->
    <div class="glass-card music-card">
      <img src="/images/music-logo.gif" alt="Music" class="icon-music">
      <h2 class="section-title"> MÚSICA </h2>
      <p class="section-subtitle">¡Que no pare la fiesta!</p>
      <p class="section-description music-description">
        Queremos que la pista de baile sea inolvidable. Ayudanos a armar la playlist perfecta subiendo una canción que no puede faltar.
      </p>

      <div class="action-buttons">
          <a :href="musicFormUrl" target="_blank" rel="noopener" class="btn-primary">SUGERIR TEMA</a>
        </div>
    </div>
  </section>
</template>

<script setup>
import { Music as MusicIcon } from '@lucide/vue';

defineProps({
  venueName: {
    type: String,
    default: 'Salón Ohana Eventos'
  },
  venueAddress: {
    type: String,
    default: 'Pozo de Vargas 2257 Ingeniero Pablo Nogués'
  },
  partyTime: {
    type: String,
    default: '18:00'
  },
  googleMapsUrl: {
    type: String,
    default: 'https://maps.google.com'
  },
  musicFormUrl: {
    type: String,
    default: 'https://docs.google.com/forms/d/1l5SdNkR4QMU7eSCcu_-eyV9s7y8l-lXmBCkzeAHFeos/edit'
  }
});
</script>

<style lang="scss" scoped>
.venue-music-section {
  display: flex;
  flex-direction: column;
  padding: 1rem 0;
}

.icon-party {
  width: 130px;
  object-fit: contain;
}

.icon-music {
  width: 90px;
  object-fit: contain;
  padding-bottom: 1.5rem;
}

.venue-name {
  font-family: $font-title;
  font-size: 1.8rem;
  font-weight: 700;
  color: $color-primary;
  margin: 0.5rem 0;
}

.venue-address {
  font-family: $font-subtitle;
  color: $color-primary;
  font-size: 1.2rem;
  margin-bottom: 0.3rem;
  padding: 0 4rem;
  line-height: 1.5rem;
}

.venue-time {
  font-family: $font-subtitle;
  color: $color-primary;
  font-size: 1.05rem;
  font-weight: 400;
  margin: 1.5rem 0 0;
  line-height: 1.7rem;
}

.venue-disclaimer {
  margin-top: 0rem;
}

.btn-wrapper {
  margin-top: 1rem;
}
</style>
