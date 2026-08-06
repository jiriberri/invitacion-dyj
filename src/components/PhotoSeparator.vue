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
  height: 420px;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;

  @media (max-width: $breakpoint-tablet) {
    height: 280px;
    background-attachment: scroll; // En mobile scroll es mejor para performance
  }
}

.separator-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
}

.separator-content {
  position: relative;
  z-index: 2;
  color: $color-white;
  text-align: center;
  padding: 0 1.5rem;
  max-width: 700px;
}

.quote-text {
  font-family: $font-title;
  font-size: 2.2rem;
  font-style: italic;
  line-height: 1.3;
  text-shadow: 0 2px 10px rgba(0,0,0,0.5);

  @media (max-width: $breakpoint-tablet) {
    font-size: 1.5rem;
  }
}
</style>
