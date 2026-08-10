<template>
  <div class="photo-separator-wrapper">
    <div class="photo-separator" :style="{ backgroundImage: `url(${imageUrl})` }">
      <div class="separator-overlay"></div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  imageUrl: {
    type: String,
    default: '/images/separator-1.jpg'
  }
});
</script>

<style lang="scss" scoped>
.photo-separator-wrapper {
  max-width: 900px;
  padding: 0 1rem;

  @media (min-width: $breakpoint-tablet) {
    padding: 0 1.5rem;
  }
}

.photo-separator {
  position: relative;
  width: 100%;
  height: 280px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: $shadow-card;
  border: 1px solid $color-border;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

  @media (min-width: $breakpoint-tablet) {
    height: 420px;
    border-radius: 24px;
  }
}

.separator-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.12);
}
</style>
