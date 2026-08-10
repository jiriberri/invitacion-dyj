<template>
  <footer class="footer-section">
    <div class="closing-image-wrapper">
      <img 
            :src="typeof closingImage === 'string' ? closingImage : closingImage.src" 
            alt="Gracias por acompañarnos" 
            class="closing-image" 
            :style="{ objectPosition: typeof closingImage === 'object' && closingImage.position ? closingImage.position : 'center' }"
          />
      <div class="closing-overlay"></div>
      <div class="closing-content">
        <h2 class="thank-you-title">¡Te Esperamos!</h2>
        <p class="couple-signature">{{ coupleNames }}</p>
        <p class="copyright">Hecho con ❤️ para celebrar nuestro día especial</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
defineProps({
  closingImage: {
    type: String,
    default: {src: '/images/closing.jpg', position: 'top'}
  },
  coupleNames: {
    type: String,
    default: 'Nombre 1 & Nombre 2'
  }
});
</script>

<style lang="scss" scoped>
.footer-section {
  width: 100%;
  margin-top: 2rem;
}

.closing-image-wrapper {
  position: relative;
  width: 100%;
  height: 50vh;
  min-height: 380px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.closing-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.closing-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.7) 0%, rgba(0,0,0,0.3) 100%);
}

.closing-content {
  position: relative;
  z-index: 2;
  color: $color-white;
  padding: 2rem 1.5rem;
}

.thank-you-title {
  font-size: 3.5rem;
  font-family: $font-title;
  margin-bottom: 0.5rem;
  text-shadow: 0 4px 15px rgba(0,0,0,0.4);

  @media (max-width: $breakpoint-tablet) {
    font-size: 2.5rem;
  }
}

.couple-signature {
  font-family: $font-title;
  font-size: 2rem;
  font-style: italic;
  color: $color-secondary;
  margin-bottom: 1.5rem;
}

.copyright {
  font-size: 0.85rem;
  opacity: 0.8;
  letter-spacing: 0.5px;
}
</style>
