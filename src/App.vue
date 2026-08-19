<template>
  <div class="wedding-invitation-app">
    <!-- Parte 1: Portada, Nombres, Mensaje, Calendario & Cuenta Regresiva -->
    <HeroSection 
      :coupleNames="weddingData.coupleNames"
      :coverImage="weddingData.coverImage"
      :weddingDateStr="weddingData.weddingDateStr"
      :weddingTime="weddingData.weddingTime"
      :weddingIsoDate="weddingData.weddingIsoDate"
      :rsvpFormUrl="weddingData.rsvpFormUrl"
    />

    <!-- Parte 2: Salón (Google Maps) & Música (Google Form) -->
    <VenueMusicSection 
      :venueName="weddingData.venueName"
      :venueAddress="weddingData.venueAddress"
      :partyTime="weddingData.weddingTime"
      :googleMapsUrl="weddingData.googleMapsUrl"
      :musicFormUrl="weddingData.musicFormUrl"
    />

    <!-- Foto Separadora 1 -->
    <PhotoSeparator 
      imageUrl="/images/separator-1.jpg"
    />

    <!-- Parte 3: Dress Code & Regalos (Alias / CBU) -->
    <DressCodeGiftSection 
      :dressCodeType="weddingData.dressCodeType"
      :dressCodeDescription="weddingData.dressCodeDescription"
      :dressCodeDisclaimer="weddingData.dressCodeDisclaimer"
      :giftMessage="weddingData.giftMessage"
      :cbu="weddingData.cbu"
      :alias="weddingData.alias"
      :bankHolder="weddingData.bankHolder"
    />

    <!-- Carrusel de fotos -->
    <PhotoCarousel />

    <!-- Parte 4: Transporte & WhatsApp -->
    <TransportSection 
      :transportDescription="weddingData.transportDescription"
      :whatsappPhone="weddingData.whatsappPhone"
      :whatsappMessage="weddingData.whatsappMessage"
    />

    <!-- Parte 5: Confirmación de asistencia -->
    <ConfirmSection
      :confirmDescription="weddingData.confirmDescription"
      :dueDate="weddingData.dueDate"
      :confirmFormUrl="weddingData.confirmFormUrl"
    />

    <!-- Cierre: Foto final -->
    <FooterSection />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import HeroSection from './components/HeroSection.vue';
import VenueMusicSection from './components/VenueMusicSection.vue';
import PhotoSeparator from './components/PhotoSeparator.vue';
import DressCodeGiftSection from './components/DressCodeGiftSection.vue';
import PhotoCarousel from './components/PhotoCarousel.vue';
import TransportSection from './components/TransportSection.vue';
import FooterSection from './components/FooterSection.vue';
import ConfirmSection from './components/ConfirmSection.vue';

// Configuración fácil de editar para los novios
const weddingData = ref({
  coupleNames: 'Dai & Juli',
  coverImage: '/images/hero-cover.jpg',
  weddingDateStr: '31 de Octubre de 2026',
  weddingTime: '21:30',
  weddingIsoDate: '2026-10-31T21:00:00',
  rsvpFormUrl: 'https://forms.google.com', // Reemplazar con el link real de Google Forms
  
  venueName: 'Salón Ohana Eventos',
  venueAddress: 'Pozo de Vargas 2257 Ingeniero Pablo Nogués',
  googleMapsUrl: 'https://maps.app.goo.gl/pwLpSPKkooLREtjAA',

  musicFormUrl: 'https://docs.google.com/forms/d/e/1FAIpQLSe7L8FKq-OOIi_AY3q6t5GG2yZ2KwPiYSXVZ6HVSDySHFzG2g/viewform?usp=publish-editor', // Link de Google Forms para sugerir música

  dressCodeType: 'Elegante Sport',
  dressCodeDescription: 'Queremos que estés súper cómodo para que puedas bailar toda la noche.',
  dressCodeDisclaimer: '¡Por favor no asistir con colores claros!',

  giftMessage: 'Tu presencia es lo único que necesitamos. Si querés hacernos un presente para nuestra luna de miel, te dejamos nuestra cuenta bancaria.',
  cbu: '0720079388000002409786',
  alias: 'PAPEL.GRADO.MONTE',
  bankHolder: 'Julián Iriberri',

  transportDescription: 'Queremos que disfrutes sin preocuparte por manejar. Si querés sumarte al traslado grupal que estamos organizando, contactate con Mica por WhatsApp.',
  whatsappPhone: '541133702865',
  whatsappMessage: '¡Hola! Quisiera consultar acerca del servicio de transporte para el casamiento de Dai y Juli.',

  confirmDescription: 'Esperamos que puedas acompañarnos en este momento tan especial.',
  dueDate: 'Te pedimos que completes este formulario antes del 30/09/2026.',
  confirmFormUrl: 'https://docs.google.com/forms/d/e/1FAIpQLScRdocg27UL3ZI8Ge_nTQ0yxavcmCrfkdoNPMNOiB7p_x-gWg/viewform?usp=publish-editor' // Link de Google Forms para confirmar asistencia
});
</script>

<style lang="scss">
// Estilos del contenedor principal
.wedding-invitation-app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  @media (min-width: $breakpoint-desktop) {
    background-color: #FFFFFF;
    max-width: 650px;
    margin: 2.5rem auto;
    border-radius: 28px;
    overflow: hidden;
    box-shadow: 0 8px 60px rgba(0, 0, 0, 0.25), 0 2px 20px rgba(0, 0, 0, 0.1);
    min-height: auto;
  }
}
</style>
