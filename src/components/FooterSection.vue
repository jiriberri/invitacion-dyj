<template>
  <footer class="footer-section">
    <div class="closing-image-wrapper">
      <img 
        :src="typeof closingImage === 'string' ? closingImage : closingImage.src" 
        alt="Gracias por acompañarnos" 
        class="closing-image" 
        :style="{ objectPosition: typeof closingImage === 'object' && closingImage.position ? closingImage.position : 'center' }"
      />
      <div class="closing-content">
        <h2 class="thank-you-title">¡Te esperamos!</h2>
      </div>
    </div>
  </footer>
</template>

<script setup>
defineProps({
  closingImage: {
    type: [String, Object],
    default: () => ({ src: '/images/closing.jpg', position: 'center' })
  }
});
</script>

<style lang="scss" scoped>
.footer-section {
  width: 100%;
  position: static;
  z-index: 4;
  margin-top: -3rem;
}

.closing-image-wrapper {
  position: relative;
  width: 100%;
  height: 75vh;
  min-height: 520px;
  max-height: 800px;
  overflow: hidden;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  text-align: center;

  @media (min-width: $breakpoint-tablet) {
    height: 85vh;
    min-height: 600px;
  }
}

.closing-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.closing-content {
  position: relative;
  z-index: 2;
  color: $color-white;
  padding: 1.5rem 1.5rem 3rem 1.5rem;
}

.thank-you-title {
  font-size: 1.8rem;
  font-family: $font-against;
  font-weight: 400;
  color: $color-white;
  margin: 0;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.6);

  @media (min-width: $breakpoint-tablet) {
    font-size: 2.5rem;
  }
}
</style>
