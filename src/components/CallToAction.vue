<!-- components/CallToAction.vue -->
<template>
  <section class="cta-wrapper">
    <div class="cta-accent-bar"></div>

    <div class="cta-inner">
      <div class="cta-text-block">
        <p class="cta-eyebrow">Masih bingung mau pilih apa?</p>
        <h2 class="cta-heading">Yuk, ngobrol dulu sama kami 🤍</h2>
        <p class="cta-subtext">
          Kami bantu kamu pilih hampers atau produk aktifitas yang pas — tinggal cerita aja anaknya umur berapa dan buat acara apa.
        </p>
      </div>

      <div class="cta-button-group">
        <a :href="waOrderLink" target="_blank" rel="noopener noreferrer" class="cta-btn-primary">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="cta-btn-icon" aria-hidden="true">
            <path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946.003-6.556 5.338-11.891 11.893-11.891 3.181.001 6.167 1.24 8.413 3.488 2.245 2.248 3.481 5.236 3.48 8.414-.003 6.557-5.338 11.892-11.893 11.892-1.99-.001-3.951-.5-5.688-1.448l-6.305 1.654zm6.597-3.807c1.676.995 3.276 1.591 5.392 1.592 5.448 0 9.886-4.434 9.889-9.885.002-5.462-4.415-9.89-9.881-9.892-5.452 0-9.887 4.434-9.889 9.884-.001 2.225.651 3.891 1.746 5.634l-.999 3.648 3.742-.981zm11.387-5.464c-.074-.124-.272-.198-.57-.347-.297-.149-1.758-.868-2.031-.967-.272-.099-.47-.149-.669.149-.198.297-.768.967-.941 1.165-.173.198-.345.223-.643.074-.297-.149-1.255-.462-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.372-.025-.521-.075-.148-.669-1.611-.916-2.206-.242-.579-.487-.501-.669-.51l-.57-.01c-.198 0-.52.074-.792.372s-1.04 1.016-1.04 2.479 1.065 2.876 1.213 3.074c.149.198 2.095 3.2 5.076 4.487.709.306 1.263.489 1.694.626.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.695.248-1.29.173-1.414z" />
          </svg>
          Mau Order Sekarang
        </a>

        <a :href="waAskLink" target="_blank" rel="noopener noreferrer" class="cta-btn-secondary">
          Tanya-tanya Dulu
        </a>
      </div>

      <p class="cta-trust-note">✨ Kami balas secepatnya dalam jam kerja ya </p>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  productContext: {
    type: String,
    default: ''
  },
  phoneNumber: {
    type: String,
    default: '6281234567890'
  }
})
const waNumber = import.meta.env.VITE_WA_NUMBER

const waOrderLink = computed(() => {
  const context = props.productContext ? `untuk *${props.productContext}*` : ''
  const msg = encodeURIComponent(
    `Halo Pepepipi! 👋\nAku mau order ${context}.\nBisa bantu aku pilih yang paling cocok?`
  )
  return `https://wa.me/${waNumber}?text=${msg}`
})

const waAskLink = computed(() => {
  const msg = encodeURIComponent(
    `Halo Pepepipi! 😊\nAku lagi lihat-lihat produknya dan ada beberapa pertanyaan nih. Boleh tanya-tanya dulu?`
  )
  return `https://wa.me/${waNumber}?text=${msg}`
})
</script>

<style scoped>
.cta-wrapper {
  background: linear-gradient(135deg, #FFF4EA 0%, #F3F8FC 100%);
  border: 1.5px solid #BDE2F7;
  border-radius: 20px;
  overflow: hidden;
  margin: 2.5rem auto;
  max-width: 680px;
  box-shadow: 0 4px 24px rgba(92, 167, 212, 0.08);
}

.cta-accent-bar {
  height: 5px;
  background: linear-gradient(90deg, #FFC89A, #5CA7D4, #BDE2F7);
}

.cta-inner {
  padding: 2.5rem 2rem;
  text-align: center;
}

.cta-eyebrow {
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #5CA7D4;
  margin-bottom: 0.5rem;
}

.cta-heading {
  font-family: 'Plus Jakarta Sans', 'Inter', sans-serif;
  font-size: clamp(1.4rem, 3.5vw, 1.9rem);
  font-weight: 800;
  color: #2d3748;
  margin-bottom: 0.75rem;
  line-height: 1.3;
}

.cta-subtext {
  font-size: 0.95rem;
  color: #718096;
  line-height: 1.7;
  max-width: 480px;
  margin: 0 auto 2rem;
}

.cta-button-group {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  justify-content: center;
  margin-bottom: 1.25rem;
}

.cta-btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background-color: #5CA7D4;
  color: #ffffff;
  font-weight: 700;
  font-size: 0.95rem;
  padding: 0.8rem 1.6rem;
  border-radius: 12px;
  text-decoration: none;
  transition: background-color 0.2s ease, transform 0.15s ease;
  box-shadow: 0 4px 12px rgba(92, 167, 212, 0.3);
}

.cta-btn-primary:hover {
  background-color: #4a90bb;
  transform: translateY(-2px);
}

.cta-btn-secondary {
  display: inline-flex;
  align-items: center;
  background-color: transparent;
  color: #5CA7D4;
  font-weight: 600;
  font-size: 0.95rem;
  padding: 0.8rem 1.6rem;
  border-radius: 12px;
  border: 1.5px solid #5CA7D4;
  text-decoration: none;
  transition: background-color 0.2s ease, transform 0.15s ease;
}

.cta-btn-secondary:hover {
  background-color: #F3F8FC;
  transform: translateY(-2px);
}

.cta-btn-icon {
  width: 18px;
  height: 18px;
  flex-shrink: 0;
}

.cta-trust-note {
  font-size: 0.8rem;
  color: #a0aec0;
  margin: 0;
}
</style>