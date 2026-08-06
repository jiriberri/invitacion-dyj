<template>
  <div class="wedding-invitation-app">
    <!-- Parte 1: Portada, Nombres, Mensaje, Calendario & Cuenta Regresiva -->
    <HeroSection 
      :coupleNames="weddingData.coupleNames"
      :shortMessage="weddingData.shortMessage"
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
      imageUrl="/images/separator-1.png"
      quote="Lo mejor de la vida es encontrar a alguien con quien compartirla"
    />

    <!-- Parte 3: Dress Code & Regalos (Alias / CBU) -->
    <DressCodeGiftSection 
      :dressCodeType="weddingData.dressCodeType"
      :dressCodeDescription="weddingData.dressCodeDescription"
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
  shortMessage: 'Nos encantaría compartir con vos la alegría de dar este gran paso juntos.',
  weddingDateStr: 'Sábado, 21 de Noviembre de 2026',
  weddingTime: '18:00',
  weddingIsoDate: '2026-11-21T18:00:00',
  rsvpFormUrl: 'https://forms.google.com', // Reemplazar con el link real de Google Forms
  
  venueName: 'Salón Quinta de las Rosas',
  venueAddress: 'Av. Las Palmas 1234, Buenos Aires',
  googleMapsUrl: 'https://maps.google.com', // Link de Google Maps

  musicFormUrl: 'https://forms.google.com', // Link de Google Forms para sugerir música

  dressCodeType: 'Elegante',
  dressCodeDescription: 'Queremos que te sientas cómodo y te luzcas para celebrar juntos esta noche inolvidable.',

  giftMessage: 'Tu presencia es nuestro mejor regalo. Si deseas realizarnos un presente para nuestra luna de miel, te compartimos nuestros datos bancarios:',
  cbu: '0000003100012345678901',
  alias: 'DAI.Y.JULI.BODA',
  bankHolder: 'Dai & Juli',

  transportDescription: 'Para tu comodidad, contaremos con servicio de transporte / combis hacia el salón.',
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
