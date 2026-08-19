<template>
  <section class="dress-gift-section section-container">
    <!-- Dress Code -->
    <div class="glass-card dress-card">
      <img src="/images/suit-logo.gif" alt="Suit" class="icon-suit">
      <p class="section-title">DRESS CODE</p>
      <p class="section-subtitle">{{ dressCodeType }}</p>
      <p class="section-description">{{ dressCodeDescription }}</p>
      <p class="dress-disclaimer">{{ dressCodeDisclaimer }}</p>
    </div>

    <!-- Regalo / Alias CBU -->
    <div class="glass-card gift-card">
      <img src="/images/gift-logo.gif" alt="Gift" class="icon-gift">
      <h2 class="section-subtitle gift-title">Nuestra luna de miel</h2>
      <p class="section-description gift-description">{{ giftMessage }}</p>

      <div class="bank-details-container">
        <div class="bank-row" v-if="cbu">
          <span class="bank-text"><span class="bank-label">CBU:</span> {{ cbu }}</span>
          <button @click="copyToClipboard(cbu, 'cbu')" class="copy-btn" title="Copiar CBU">
            <CheckIcon v-if="copiedField === 'cbu'" class="check-icon" />
            <CopyIcon v-else class="copy-icon" />
          </button>
        </div>

        <div class="bank-row alias" v-if="alias">
          <span class="bank-text"><span class="bank-label">Alias:</span> {{ alias }}</span>
          <button @click="copyToClipboard(alias, 'alias')" class="copy-btn" title="Copiar Alias">
            <CheckIcon v-if="copiedField === 'alias'" class="check-icon" />
            <CopyIcon v-else class="copy-icon" />
          </button>
        </div>

        <div class="bank-titular-row" v-if="bankHolder">
          <span class="bank-label">Titular:</span> {{ bankHolder }}
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
import { Copy as CopyIcon, Check as CheckIcon } from '@lucide/vue';

defineProps({
  dressCodeType: {
    type: String,
    default: 'Elegante Sport'
  },
  dressCodeDescription: {
    type: String,
    default: 'Queremos que estés súper cómodo para que puedas bailar toda la noche.'
  },
  dressCodeDisclaimer: {
    type: String,
    default: '¡Por favor no asistir con colores claros!'
  },
  giftMessage: {
    type: String,
    default: 'Tu presencia es lo único que necesitamos. Si querés hacernos un presente para nuestra luna de miel, te dejamos nuestra cuenta bancaria.'
  },
  cbu: {
    type: String,
    default: '0720079388000002409786'
  },
  alias: {
    type: String,
    default: 'PAPEL.GRADO.MONTE'
  },
  bankHolder: {
    type: String,
    default: 'Julian Iriberri'
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
}

.icon-suit {
  width: 130px;
  object-fit: contain;
  padding-bottom: 1rem;

  @media (min-width: $breakpoint-desktop) {
    width: 150px;
  }
}

.dress-disclaimer {
  display: inline-block;
  font-family: $font-subtitle;
  text-align: center;
  color: $color-primary;
  font-size: 1.05rem;
  line-height: 1.7rem;

  @media (min-width: $breakpoint-desktop) {
    font-size: 1.15rem;
  }
}

.gift-card {
  margin-top: 2rem;
  padding-top: 2.5rem;
  padding-bottom: 4rem;
  position: relative;
  z-index: 3;
  background-color: transparent !important;
  background-image: url('/images/green-back.png');
  background-size: 100% 100%;
  background-repeat: no-repeat;

  // Overflow both sides so scalloped edges go off-screen, stays centered
  width: 130%;
  margin-left: -15%;

  color: #FFFFFF;

  @media (min-width: $breakpoint-tablet) {
    background-color: $color-primary !important;
    background-image: none;
    border-radius: 24px;
    padding: 3rem 2rem;
  }

  @media (min-width: $breakpoint-desktop) {
    width: 115%;
    margin-left: -7.5%;
    border-radius: 0;
    padding: 2.5rem 2rem 3.5rem;
  }

  .icon-gift {
    width: 130px;
    object-fit: contain;

    @media (min-width: $breakpoint-desktop) {
      width: 150px;
    }
  }

  .gift-title, .gift-description {
    color: #FFFFFF;
  }
  .gift-title {
    margin-top: 0;
  }

  .gift-description {
    margin: 0.5rem 5rem;
    font-size: 1.1rem;

    @media (min-width: $breakpoint-desktop) {
      margin: 0.8rem 4rem;
      font-size: 1.2rem;
    }
  }
}


.bank-details-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  margin-top: 2rem;
  font-family: $font-title;
  font-size: 1.1rem;
  color: $color-card-bg;

  @media (min-width: $breakpoint-desktop) {
    font-size: 1.2rem;
    gap: 0.6rem;
  }
}

.bank-row {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  font-weight: 700;
  line-height: 1.9rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.15rem;
    gap: 0.8rem;
  }
}

.alias {
  gap: 0.8rem;
}

.bank-text {
  display: inline-flex;
  gap: 0.4rem;
  align-items: center;
  word-break: break-all;
}

.bank-label {
  font-weight: 700;
  opacity: 0.95;
}

.bank-titular-row {
  font-size: 0.95rem;
  font-weight: 700;
  text-align: center;
  margin-top: 0.1rem;

  @media (min-width: $breakpoint-tablet) {
    font-size: 1.15rem;
  }
}

.copy-btn {
  background: $color-card-bg;
  color: $color-primary;
  border: none;
  border-radius: 8px;
  width: 26px;
  height: 26px;
  padding: 0;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  flex-shrink: 0;
  transition: $transition-smooth;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);

  &:hover {
    background: #FFFFFF;
    transform: scale(1.1);
  }

  .copy-icon, .check-icon {
    width: 15px;
    height: 15px;
  }

  .check-icon {
    color: #2e7d32;
  }

  svg {
    color: $color-primary;
  }
}

.copy-toast {
  margin-top: 1rem;
  color: #FEFBE3;
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  text-align: center;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
