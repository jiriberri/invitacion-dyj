<template>
  <div class="countdown-container">
    <div class="countdown-item">
      <span class="number">{{ days }}</span>
      <span class="label">Días</span>
    </div>
    <div class="separator">:</div>
    <div class="countdown-item">
      <span class="number">{{ hours }}</span>
      <span class="label">Horas</span>
    </div>
    <div class="separator">:</div>
    <div class="countdown-item">
      <span class="number">{{ minutes }}</span>
      <span class="label">Minutos</span>
    </div>
    <div class="separator">:</div>
    <div class="countdown-item">
      <span class="number">{{ seconds }}</span>
      <span class="label">Segundos</span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const props = defineProps({
  targetDate: {
    type: String,
    required: true // Formato ISO, ej: "2026-11-20T18:00:00"
  }
});

const days = ref('00');
const hours = ref('00');
const minutes = ref('00');
const seconds = ref('00');

let timer = null;

const updateCountdown = () => {
  const target = new Date(props.targetDate).getTime();
  const now = new Date().getTime();
  const difference = target - now;

  if (difference <= 0) {
    days.value = '00';
    hours.value = '00';
    minutes.value = '00';
    seconds.value = '00';
    clearInterval(timer);
    return;
  }

  const d = Math.floor(difference / (1000 * 60 * 60 * 24));
  const h = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  const m = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
  const s = Math.floor((difference % (1000 * 60)) / 1000);

  days.value = String(d).padStart(2, '0');
  hours.value = String(h).padStart(2, '0');
  minutes.value = String(m).padStart(2, '0');
  seconds.value = String(s).padStart(2, '0');
};

onMounted(() => {
  updateCountdown();
  timer = setInterval(updateCountdown, 1000);
});

onUnmounted(() => {
  if (timer) clearInterval(timer);
});
</script>

<style lang="scss" scoped>
.countdown-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  margin: 2rem 0;

  @media (max-width: $breakpoint-tablet) {
    gap: 0.4rem;
  }
}

.countdown-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(255, 255, 255, 0.95);
  border: 1px solid $color-border;
  border-radius: 16px;
  padding: 1rem 1.2rem;
  min-width: 75px;
  box-shadow: $shadow-card;

  @media (max-width: $breakpoint-tablet) {
    min-width: 60px;
    padding: 0.8rem 0.6rem;
  }

  .number {
    font-family: $font-title;
    font-size: 2.2rem;
    font-weight: 700;
    color: $color-primary;
    line-height: 1;

    @media (max-width: $breakpoint-tablet) {
      font-size: 1.6rem;
    }
  }

  .label {
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: $color-text-muted;
    margin-top: 0.4rem;

    @media (max-width: $breakpoint-tablet) {
      font-size: 0.65rem;
    }
  }
}

.separator {
  font-family: $font-title;
  font-size: 1.8rem;
  font-weight: 700;
  color: $color-primary;
  margin-bottom: 1rem;
}
</style>
