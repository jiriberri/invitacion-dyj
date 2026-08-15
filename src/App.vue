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

    <!-- Cierre: Foto final -->
    <FooterSection 
      :coupleNames="weddingData.coupleNames"
    />
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

  musicFormUrl: 'https://forms.google.com', // Link de Google Forms para sugerir música

  dressCodeType: 'Elegante Sport',
  dressCodeDescription: 'Queremos que estes súper comodo para que puedas bailar toda la noche.',
  dressCodeDisclaimer: '¡Por favor no asistir con colores claros!',

  giftMessage: 'Tu presencia es lo único que necesitamos. Si queres hacernos un presente te para nuestra luna de miel, dejamos nuestra cuenta bancaria.',
  cbu: '0720079388000002409786',
  alias: 'PAPEL.GRADO.MONTE',
  bankHolder: 'Julián Iriberri',

  transportDescription: 'Queremos que disfrutes sin preocuparte por manejar. Si querés sumarte al traslado grupal que estamos organizando, contactate con Mica por WhatsApp.',
  whatsappPhone: '5491112345678',
  whatsappMessage: '¡Hola! Quisiera consultar acerca del servicio de transporte para la boda de Dai y Juli.'
});
</script>

<style lang="scss">
// Estilos del contenedor principal
.wedding-invitation-app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>
