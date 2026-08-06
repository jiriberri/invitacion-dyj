<template>
  <section class="venue-music-section section-container">
    <!-- Ubicación del Salón -->
    <div class="glass-card venue-card">
      <div class="icon-circle">
        <MapPinIcon class="icon" />
      </div>
      <h2 class="section-title">Fiesta & Celebración</h2>
      <p class="venue-name">{{ venueName }}</p>
      <p class="venue-address">{{ venueAddress }}</p>
      <p class="venue-time">Horario: {{ partyTime }} hs</p>
      
      <div class="btn-wrapper">
        <a :href="googleMapsUrl" target="_blank" rel="noopener" class="btn-primary">
          <NavigationIcon /> ¿Cómo llegar? (Google Maps)
        </a>
      </div>
    </div>

    <!-- Sugerencia de Música -->
    <div class="glass-card music-card">
      <div class="icon-circle">
        <MusicIcon class="icon" />
      </div>
      <h2 class="section-title">¿Qué tema no puede faltar?</h2>
      <p class="section-subtitle">
        ¡Queremos que bailes toda la noche! Ayudanos a armar la playlist perfecta sugiriendo tu canción favorita.
      </p>

      <div class="btn-wrapper">
        <a :href="musicFormUrl" target="_blank" rel="noopener" class="btn-secondary">
          <DiscIcon /> Recomendar una canción
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { MapPin as MapPinIcon, Navigation as NavigationIcon, Music as MusicIcon, Disc as DiscIcon } from '@lucide/vue';

defineProps({
  venueName: {
    type: String,
    default: 'Salón Quinta de las Rosas'
  },
  venueAddress: {
    type: String,
    default: 'Av. Las Palmas 1234, Buenos Aires, Argentina'
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
    default: 'https://forms.google.com'
  }
});
</script>

<style lang="scss" scoped>
.venue-music-section {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.icon-circle {
  width: 55px;
  height: 55px;
  background: rgba(184, 147, 85, 0.12);
  color: $color-primary;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1rem auto;

  .icon {
    width: 26px;
    height: 26px;
  }
}

.venue-name {
  font-family: $font-title;
  font-size: 1.8rem;
  font-weight: 700;
  color: $color-text;
  margin-top: 0.5rem;
}

.venue-address {
  font-size: 1rem;
  color: $color-text-muted;
  margin-bottom: 0.3rem;
}

.venue-time {
  font-size: 0.95rem;
  font-weight: 600;
  color: $color-primary;
  margin-bottom: 1.5rem;
}

.btn-wrapper {
  margin-top: 1rem;
}

.music-card {
  border-left: 4px solid $color-primary;
}
</style>
