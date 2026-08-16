<template>
  <section class="confirm-section section-container">
    <div class="glass-card confirm-card">
      <h2 class="section-title confirm-title">CONFIRMAR ASISTENCIA</h2>
      <p class="section-subtitle">¡Compartí con nosotros!</p>
      <p class="section-description confirm-description">{{ confirmDescription }}</p>
      <p class="section-description confirm-due-date">{{ dueDate }}</p>

      <div class="action-buttons">
          <a :href="confirmFormUrl" target="_blank" rel="noopener" class="btn-primary">CONFIRMAR</a>
      </div>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  confirmDescription: {
    type: String,
    default: 'Esperamos que puedas acompañarnos en este momento tan especial.'
  },
  dueDate: {
    type: String,
    default: 'Te pedimos que completes este formulario antes del 30/09/2026.'
  },
  confirmFormUrl: {
    type: String,
    default: 'https://forms.google.com'
  }
});
</script>

<style lang="scss" scoped>
.confirm-section {
    max-width: 100%;
    padding-bottom: 0;

    .confirm-card {
        margin-top: -2.8rem;
        position: relative;
        z-index: 3;
        background-color: transparent !important;
        background-image: url('/images/beige-back.png');
        background-size: 100% 100%;
        background-repeat: no-repeat;

        // Overflow both sides so scalloped edges go off-screen, stays centered
        width: 130%;
        margin-left: -15%;
        padding-bottom: 4rem;
    }
    .confirm-title {
      padding-top: 2rem;
        font-size: 1.3rem;
    }

    .confirm-description {
        margin: 1rem 5rem;
    }

    .confirm-due-date {
        font-size: 1rem;
        line-height: 1.7rem;
        margin: 0rem 6rem 1rem;
    }
}
</style>
