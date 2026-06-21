<template>
  <section id="simulator" class="max-w-6xl mx-auto px-4 py-12">
    <!-- Background Card menggunakan Soft Blue/Orange tint -->
    <div class="bg-white rounded-3xl p-6 md:p-10 border border-[#BDE2F7] shadow-xs">
      
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        
        <!-- Kolom Kiri: Form Filter Dropdown -->
        <div class="lg:col-span-4 space-y-6">
          <div class="flex items-center gap-3">
            <!-- Box Ikon Oranye Pastel sesuai token baru -->
            <div class="bg-[#FFC89A] p-2.5 rounded-xl text-[#0c447c]">
              🔍
            </div>
            <div>
              <h2 class="text-xl font-bold text-slate-800">Bingung Main Apa?</h2>
              <p class="text-xs text-slate-500">Temukan ide aktivitas si kecil.</p>
            </div>
          </div>

          <div class="space-y-4">
            <div>
              <label class="block text-xs font-bold text-slate-600 uppercase tracking-wide mb-1">Usia Anak</label>
              <select v-model="filter.usia" class="w-full bg-[#F3F8FC] border border-[#BDE2F7] rounded-xl px-4 py-3 text-sm text-slate-700 focus:outline-none focus:border-[#d97706]">
                <option value="3 Tahun">3 Tahun</option>
                <option value="5 Tahun">5 Tahun</option>
              </select>
            </div>
            
            <div>
              <label class="block text-xs font-bold text-slate-600 uppercase tracking-wide mb-1">Durasi</label>
              <select v-model="filter.durasi" class="w-full bg-[#F3F8FC] border border-[#BDE2F7] rounded-xl px-4 py-3 text-sm text-slate-700 focus:outline-none focus:border-[#d97706]">
                <option value="20 Menit">20 Menit</option>
                <option value="45 Menit">45 Menit</option>
              </select>
            </div>

            <div>
              <label class="block text-xs font-bold text-slate-600 uppercase tracking-wide mb-1">Lokasi</label>
              <select v-model="filter.lokasi" class="w-full bg-[#F3F8FC] border border-[#BDE2F7] rounded-xl px-4 py-3 text-sm text-slate-700 focus:outline-none focus:border-[#d97706]">
                <option value="Dalam Rumah">Dalam Rumah</option>
                <option value="Luar Rumah">Luar Rumah</option>
              </select>
            </div>
          </div>

          <!-- Tombol bertema Pastel Blue -->
          <button @click="cariIde" class="w-full bg-[#BDE2F7] text-[#0c447c] font-bold py-3.5 rounded-2xl hover:bg-[#a6d5f2] shadow-xs transition-all flex justify-center items-center gap-2">
            <span>Cari Ide Aktivitas</span> 🚀
          </button>
        </div>

        <!-- Kolom Tengah: Rekomendasi Ide -->
        <div class="lg:col-span-4">
          <p class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3">📍 Rekomendasi Ide</p>
          <div v-if="hasilIde" class="bg-[#F3F8FC] border border-[#BDE2F7] rounded-2xl p-4 shadow-xs">
            <img :src="hasilIde.foto_aktivitas" class="w-full h-44 object-cover rounded-xl mb-4" alt="Ide Main">
            <h3 class="font-bold text-base text-slate-800 mb-2">{{ hasilIde.judul_aktivitas }}</h3>
            <div class="space-y-1 text-xs text-slate-500 mb-4">
              <p>⏱️ {{ hasilIde.durasi }}</p>
              <p>🏠 {{ hasilIde.lokasi }}</p>
            </div>
            <button class="w-full border border-[#FFC89A] text-[#633806] font-medium py-2 rounded-xl text-sm bg-[#faeeda] hover:bg-[#FFC89A]/40">
              Lihat Detail
            </button>
          </div>
          <div v-else class="bg-slate-50 border border-dashed border-slate-200 rounded-2xl p-8 text-center text-xs text-slate-400">
            Pilih filter di kiri lalu klik Cari Ide
          </div>
        </div>

        <!-- Kolom Kanan: Produk yang Dibutuhkan -->
        <div class="lg:col-span-4">
          <p class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-3">🛍️ Produk yang Dibutuhkan</p>
          <div v-if="hasilIde && bahanBaku.length > 0" class="space-y-4">
            <div class="grid grid-cols-3 gap-2">
              <div v-for="item in bahanBaku" :key="item.id" class="bg-white border border-slate-100 rounded-xl p-2 text-center shadow-xs">
                <div class="w-full h-14 bg-slate-50 rounded-lg mb-1 flex items-center justify-center overflow-hidden">
                  <img :src="item.foto_url" class="object-cover max-h-full max-w-full">
                </div>
                <p class="text-[10px] font-medium text-slate-700 truncate">{{ item.nama_barang }}</p>
                <p class="text-[9px] text-[#d97706] font-bold">Rp {{ item.harga.toLocaleString('id-ID') }}</p>
              </div>
            </div>
            
            <a :href="generateWaLink" target="_blank" class="block w-full text-center bg-emerald-600 text-white font-semibold py-3 rounded-xl text-sm hover:bg-emerald-700 shadow-xs transition-all">
              Beli Paket Bahan via WA 💬
            </a>
          </div>
          <div v-else class="bg-slate-50 border border-dashed border-slate-200 rounded-2xl p-8 text-center text-xs text-slate-400">
            Bahan produk akan muncul setelah ide ditemukan
          </div>
        </div>

      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import { supabase } from '../utils/supabase'

const filter = ref({
  usia: '5 Tahun',
  durasi: '20 Menit',
  lokasi: 'Dalam Rumah'
})

const hasilIde = ref(null)
const bahanBaku = ref([])

async function cariIde() {
  const { data: ide } = await supabase
    .from('activity_ideas')
    .select('*')
    .eq('usia', filter.value.usia)
    .eq('durasi', filter.value.durasi)
    .eq('lokasi', filter.value.lokasi)
    .eq('is_active', true)
    .maybeSingle()

  hasilIde.value = ide

  if (ide) {
    const { data: bahan } = await supabase
      .from('activity_materials')
      .select('*')
      .eq('activity_id', ide.id)
    bahanBaku.value = bahan || []
  } else {
    bahanBaku.value = []
    alert("Ide belum tersedia untuk kombinasi filter ini.")
  }
}

const generateWaLink = computed(() => {
  if (!hasilIde.value) return '#'
  const listBahan = bahanBaku.value.map(b => b.nama_barang).join(', ')
  const templateTeks = `Halo Pepepipi, saya mau pesan paket bahan untuk aktivitas "${hasilIde.value.judul_aktivitas}" (${filter.value.usia}).`
  return `https://wa.me/6281234567890?text=${encodeURIComponent(templateTeks)}`
})
</script>