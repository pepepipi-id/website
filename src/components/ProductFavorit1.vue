<template>
  <section id="activities" class="max-w-6xl mx-auto px-4 py-12">
    <div class="mb-8">
      <h2 class="text-2xl font-black text-[#1e293b] tracking-tight">
        Aktivitas Anak Paling Seru
      </h2>
      <p class="text-xs font-semibold text-[#64748b] uppercase tracking-wider mt-1">
        🔥 Paling Banyak Dicari Pekan Ini
      </p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <div 
        v-for="item in products" 
        :key="item.id" 
        class="bg-[#F3F8FC] border border-[#BDE2F7] rounded-2xl p-5 shadow-xs hover:shadow-md transition-all duration-200 transform hover:-translate-y-1 flex flex-col justify-between"
      >
        <div>
          <div class="w-full h-48 bg-white rounded-xl overflow-hidden mb-4 border border-[#BDE2F7]/40">
            <img :src="item.foto_url" class="w-full h-full object-cover" :alt="item.nama_produk">
          </div>
          
          <div class="flex items-center justify-between gap-2 mb-2">
            <span class="bg-[#BDE2F7] text-[#0c447c] text-[10px] font-bold px-2.5 py-1 rounded-md uppercase tracking-wide">
              {{ item.label_terjual }}
            </span>
            <span class="text-xs font-bold text-[#d97706]">
              Rp {{ item.harga.toLocaleString('id-ID') }}
            </span>
          </div>
          <h3 class="font-bold text-base text-[#1e293b] mb-4 leading-snug">
            {{ item.nama_produk }}
          </h3>
        </div>

        <a 
          :href="'https://wa.me/6281234567890?text=' + encodeURIComponent('Halo Pepepipi, saya tertarik untuk memesan produk Aktivitas: Beli ' + item.nama_produk)"
          target="_blank"
          class="block w-full text-center bg-[#0c447c] text-white text-xs font-bold py-3 rounded-xl hover:bg-[#0b3a69] transition-all"
        >
          Pesan via WA 💬
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../utils/supabase'

const products = ref([])

onMounted(async () => {
  try {
    // 1. Ambil data produk aktivitas anak
    const { data: aktivitas, error: errAktivitas } = await supabase
      .from('products')
      .select('*')
      .eq('kategori', 'Aktivitas') // Pastikan 'Aktivitas' pakai huruf kapital sesuai DB
      .eq('is_active', true)
      .limit(3)
    
    if (errAktivitas) {
      console.error("Terjadi error pada fetch aktivitas:", errAktivitas)
    }
    hasAktivitas.value = aktivitas && aktivitas.length > 0

    // 2. Ambil data produk hampers
    const { data: hampers, error: errHampers } = await supabase
      .from('products')
      .select('*')
      .eq('kategori', 'Hampers') // Pastikan 'Hampers' pakai huruf kapital sesuai DB
      .eq('is_active', true)
      .limit(3)
    
    if (errHampers) {
      console.error("Terjadi error pada fetch hampers:", errHampers)
    }
    hasHampers.value = hampers && hampers.length > 0

  } catch (error) {
    console.error("Gagal memuat data, tetapi web tetap aman tampil:", error)
  }
})
</script>