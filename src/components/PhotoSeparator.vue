<template>
  <div class="photo-separator" :style="{ backgroundImage: `url(${imageUrl})` }">
    <div class="separator-overlay"></div>
    <div class="separator-content" v-if="quote">
      <p class="quote-text">"{{ quote }}"</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  imageUrl: {
    type: String,
    default: '/images/separator-1.png'
  },
  quote: {
    type: String,
    default: ''
  }
});
</script>

<style lang="scss" scoped>
.photo-separator {
  position: relative;
  width: 100%;
  height: 260px;
  background-attachment: scroll; // En mobile scroll mejora el rendimiento
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;

  @media (min-width: $breakpoint-tablet) {
    height: 400px;
    background-attachment: fixed; // Parallax en pantallas grandes
  }
}

.separator-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.45);
}

.separator-content {
  position: relative;
  z-index: 2;
  color: $color-white;
  text-align: center;
  padding: 0 1.2rem;
  max-width: 700px;
}

.quote-text {
  font-family: $font-title;
  font-size: 1.4rem;
  font-style: italic;
  line-height: 1.35;
  text-shadow: 0 2px 10px rgba(0,0,0,0.5);

  @media (min-width: $breakpoint-tablet) {
    font-size: 2.2rem;
  }
}
</style>
