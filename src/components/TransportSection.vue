<template>
  <section class="transport-section section-container">
    <div class="glass-card transport-card">
      <h2 class="section-title">TRANSPORTE</h2>
      <p class="section-subtitle">¿Necesitas transporte?</p>
      <p class="section-description transport-description">{{ transportDescription }}</p>

      <div class="action-buttons">
        <a :href="whatsappUrl" target="_blank" rel="noopener" class="btn-primary">CONTACTAR</a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  transportDescription: {
    type: String,
    default: 'Queremos que disfrutes sin preocuparte por manejar. Si querés sumarte al traslado grupal que estamos organizando, contactate con Mica por WhatsApp.'
  },
  whatsappPhone: {
    type: String,
    default: '5491112345678'
  },
  whatsappMessage: {
    type: String,
    default: '¡Hola! Quisiera consultar acerca del servicio de transporte para la boda.'
  }
});

const whatsappUrl = computed(() => {
  const encodedMsg = encodeURIComponent(props.whatsappMessage);
  return `https://wa.me/${props.whatsappPhone}?text=${encodedMsg}`;
});
</script>

<style lang="scss" scoped>
.transport-section .transport-card .section-title {
  line-height: 3rem;
  font-size: 1.6rem;
}

.transport-description {
  margin: 0.5rem 0;
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

.btn-whatsapp {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  background: #25d366;
  color: $color-white;
  padding: 0.9rem 2rem;
  border-radius: 50px;
  font-size: 0.95rem;
  font-weight: 600;
  letter-spacing: 0.5px;
  box-shadow: 0 4px 20px rgba(37, 211, 102, 0.35);
  transition: $transition-smooth;

  &:hover {
    background: #20ba5a;
    transform: translateY(-3px);
    box-shadow: 0 8px 25px rgba(37, 211, 102, 0.5);
  }

  svg {
    width: 1.2rem;
    height: 1.2rem;
  }
}
</style>
