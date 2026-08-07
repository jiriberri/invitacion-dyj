<template>
  <section class="dress-gift-section section-container">
    <!-- Dress Code -->
    <div class="glass-card dress-card">
      <div class="icon-circle">
        <SparklesIcon class="icon" />
      </div>
      <h2 class="section-title">Dress Code</h2>
      <p class="dress-type">{{ dressCodeType }}</p>
      <p class="section-subtitle">{{ dressCodeDescription }}</p>
      <p class="dress-disclaimer">{{ dressCodeDisclaimer }}</p>
    </div>

    <!-- Regalo / Alias CBU -->
    <div class="glass-card gift-card">
      <div class="icon-circle">
        <GiftIcon class="icon" />
      </div>
      <h2 class="section-title">Regalos</h2>
      <p class="section-subtitle">{{ giftMessage }}</p>

      <div class="bank-details-box">
        <div class="detail-row" v-if="cbu">
          <span class="detail-label">CBU:</span>
          <span class="detail-value">{{ cbu }}</span>
          <button @click="copyToClipboard(cbu, 'cbu')" class="copy-btn" title="Copiar CBU">
            <CheckIcon v-if="copiedField === 'cbu'" class="check-icon" />
            <CopyIcon v-else class="copy-icon" />
          </button>
        </div>

        <div class="detail-row" v-if="alias">
          <span class="detail-label">Alias:</span>
          <span class="detail-value highlight">{{ alias }}</span>
          <button @click="copyToClipboard(alias, 'alias')" class="copy-btn" title="Copiar Alias">
            <CheckIcon v-if="copiedField === 'alias'" class="check-icon" />
            <CopyIcon v-else class="copy-icon" />
          </button>
        </div>

        <div class="detail-row" v-if="bankHolder">
          <span class="detail-label">Titular:</span>
          <span class="detail-value">{{ bankHolder }}</span>
          <span class="copy-btn-placeholder"></span>
        </div>
      </div>

      <transition name="fade">
        <p v-if="copiedField" class="copy-toast">¡Copiado al portapapeles con éxito!</p>
      </transition>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import { Sparkles as SparklesIcon, Gift as GiftIcon, Copy as CopyIcon, Check as CheckIcon } from '@lucide/vue';

defineProps({
  dressCodeType: {
    type: String,
    default: 'Elegante Sport'
  },
  dressCodeDescription: {
    type: String,
    default: '¡Queremos que estés comodo!'
  },
  dressCodeDisclaimer: {
    type: String,
    default: 'No vengas con colores claros'
  },
  giftMessage: {
    type: String,
    default: 'El mejor regalo es tu presencia. Si deseas hacernos un obsequio para nuestra luna de miel, te dejamos nuestros datos bancarios:'
  },
  cbu: {
    type: String,
    default: '0000003100012345678901'
  },
  alias: {
    type: String,
    default: 'NUESTRA.BODA.2026'
  },
  bankHolder: {
    type: String,
    default: 'Nombre 1 & Nombre 2'
  }
});

const copiedField = ref(null);

const copyToClipboard = (text, fieldName) => {
  navigator.clipboard.writeText(text).then(() => {
    copiedField.value = fieldName;
    setTimeout(() => {
      copiedField.value = null;
    }, 2500);
  });
};
</script>

<style lang="scss" scoped>
.dress-gift-section {
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

.dress-type {
  font-family: $font-title;
  font-size: 1.8rem;
  font-weight: 700;
  color: $color-primary;
  margin: 0.3rem 0 1rem 0;
}

.bank-details-box {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid $color-border;
  border-radius: 16px;
  padding: 1.5rem;
  max-width: 500px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.detail-row {
  display: grid;
  grid-template-columns: 65px 1fr 34px;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.95rem;

  .detail-label {
    font-weight: 600;
    color: $color-text-muted;
    text-align: left;
  }

  .detail-value {
    font-weight: 600;
    color: $color-text;
    text-align: center;
    word-break: break-all;

    &.highlight {
      color: $color-primary;
      font-weight: 700;
      letter-spacing: 0.5px;
    }
  }
}

.copy-btn-placeholder {
  width: 34px;
  height: 34px;
  display: inline-block;
}

.copy-btn {
  background: rgba(184, 147, 85, 0.1);
  color: $color-primary;
  border-radius: 8px;
  padding: 0.4rem 0.6rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: $transition-smooth;

  &:hover {
    background: $color-primary;
    color: $color-white;
  }

  .copy-icon, .check-icon {
    width: 16px;
    height: 16px;
  }

  .check-icon {
    color: #2e7d32;
  }
}

.copy-toast {
  margin-top: 1rem;
  color: #2e7d32;
  font-weight: 600;
  font-size: 0.9rem;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
