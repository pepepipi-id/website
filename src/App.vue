<template>
 

  <!-- Menggunakan latar belakang #FAFAF8 sesuai token --color-background-primary baru -->
  <div  class="min-h-screen bg-[#FAFAF8] text-gray-800 antialiased font-sans">
    <!-- 1. Header/Navbar -->
    <Navbar />

    <!-- 2. Banner Utama -->
    <MainBanner />

    <!-- 3. Aktivitas Anak Favorit -->
    <ProductFavorit1 v-if="hasAktivitas" />

    <!-- 4. Hampers Favorit -->
    <ProductFavorit2 v-if="hasHampers" />

    <!-- 5. Simulasi Aktivitas -->
    <ActivitySimulator v-if="false" /> <!-- masukkan "hasSimulasi" jika tersedia -->

    <!-- 6. Testimoni -->
    <Testimoni v-if="hasTestimoni" />

    <!-- 7. CTA WhatsApp Utama -->
    <CallToAction />

    <!-- CTA kontekstual — setelah user lihat kategori Hampers
     <CallToAction :product-context="hampers ultah anak" /> -->
    

    <!-- CTA setelah Activity Simulator generate hasil 
     <CallToAction product-context="simulatorResult.activityName" />
     -->
    

    <!-- 8. Footer Pepepipi -->
    <MainFooter />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from './utils/supabase'

// Import Semua Komponen Utama
import Navbar from './components/Navbar.vue'
import MainBanner from './components/MainBanner.vue'
import ProductFavorit1 from './components/ProductFavorit1.vue'
import ProductFavorit2 from './components/ProductFavorit2.vue'
import ActivitySimulator from './components/ActivitySimulator.vue'
import Testimoni from './components/Testimoni.vue'
import CallToAction from './components/CallToAction.vue'
import MainFooter from './components/MainFooter.vue'

const waNumber = import.meta.env.VITE_WA_NUMBER

// ====== FIX: Import & State untuk Panel Admin ======
import AdminPanel from './components/AdminPanel.vue'
const showAdmin = ref(false)
// ===================================================

// Status apakah data ada di Supabase (default true agar kita bisa desain dulu)
const hasAktivitas = ref(true)
const hasHampers = ref(true)
const hasSimulasi = ref(true)
const hasTestimoni = ref(true)

// Logika mengambil data asli dari Supabase saat halaman di-load
onMounted(async () => {
  try {
    // Contoh cek data produk aktivitas anak
    const { data: aktivitas, error: errAktivitas } = await supabase
  .from('products')
  .select('*')
  .eq('kategori', 'Aktivitas')
  .eq('is_active', true)
  .limit(3)

if (errAktivitas) {
  console.error("Error Aktivitas:", errAktivitas)
}
    console.log("Data Aktivitas dari Supabase:", aktivitas)

    hasAktivitas.value = aktivitas && aktivitas.length > 0

    // Contoh cek data produk hampers
    const { data: hampers, error: errHampers } = await supabase
  .from('products')
  .select('*')
  .eq('kategori', 'Hampers')
  .eq('is_active', true)
  .limit(3)

if (errHampers) {
  console.error("Error Hampers:", errHampers)
}
console.log("Data Hampers dari Supabase:", hampers)

    hasHampers.value = hampers && hampers.length > 0

    // (Logika pengecekan data simulasi & testimoni akan berjalan otomatis di sini nanti)
  } catch (error) {
    console.error("Gagal memuat data, tetapi web tetap aman tampil:", error)
  }
})
</script>