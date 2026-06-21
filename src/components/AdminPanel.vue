<template>
  <div class="max-w-2xl mx-auto my-10 p-6 bg-white rounded-2xl shadow-sm border border-slate-100">
    <h2 class="text-2xl font-bold text-main-dark mb-6 text-center">✨ Input Produk Pepepipi</h2>
    
    <!-- Notifikasi Sukses/Gagal -->
    <div v-if="statusMessage" :class="isSuccess ? 'bg-green-50 text-green-700' : 'bg-red-50 text-red-700'" class="p-4 rounded-xl mb-4 text-sm font-medium">
      {{ statusMessage }}
    </div>

    <form @submit.prevent="handleSubmit" class="space-y-4">
      <!-- Nama Produk -->
      <div>
        <label class="block text-sm font-semibold text-main-dark mb-1">Nama Produk / Aktivitas</label>
        <input v-model="form.nama" type="text" placeholder="Contoh: Sensory Play Kit" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:border-[#5CA7D4]" required />
      </div>

      <!-- Kategori (Dropdown) -->
      <div>
        <label class="block text-sm font-semibold text-main-dark mb-1">Kategori</label>
        <select v-model="form.kategori" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:border-[#5CA7D4]" required>
          <option value="aktivitas">Aktivitas Anak (Kartu Biru)</option>
          <option value="hampers">Paket Hampers (Kartu Oranye)</option>
        </select>
      </div>

      <!-- Harga -->
      <div>
        <label class="block text-sm font-semibold text-main-dark mb-1">Harga (Rp)</label>
        <input v-model.number="form.harga" type="number" placeholder="Contoh: 85000" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:border-[#5CA7D4]" required />
      </div>

      <!-- Deskripsi -->
      <div>
        <label class="block text-sm font-semibold text-main-dark mb-1">Deskripsi</label>
        <textarea v-model="form.deskripsi" rows="3" placeholder="Jelaskan detail produk di sini..." class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:border-[#5CA7D4]" required></textarea>
      </div>

      <!-- URL Gambar -->
      <div>
        <label class="block text-sm font-semibold text-main-dark mb-1">Link URL Gambar</label>
        <input v-model="form.gambar_url" type="url" placeholder="https://link-foto-kamu.com/gambar.jpg" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:border-[#5CA7D4]" />
      </div>

      <!-- Tombol Submit -->
      <button type="submit" :disabled="loading" class="w-full btn-primary-pastel py-3 rounded-xl font-bold shadow-md transition disabled:opacity-50">
        {{ loading ? 'Menyimpan ke Database...' : '🚀 Simpan ke Supabase' }}
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { supabase } from '../utils/supabase' // Sesuaikan path utils kamu

const form = ref({
  nama: '',
  kategori: 'aktivitas',
  harga: null,
  deskripsi: '',
  gambar_url: ''
})

const loading = ref(false)
const statusMessage = ref('')
const isSuccess = ref(true)

const handleSubmit = async () => {
  loading.value = true
  statusMessage.value = ''
  
  try {
    const { data, error } = await supabase
      .from('products')
      .insert([
        { 
          nama: form.value.nama,
          kategori: form.value.kategori,
          harga: form.value.harga,
          deskripsi: form.value.deskripsi,
          gambar_url: form.value.gambar_url || 'https://placeholder.co/300x300'
        }
      ])

    if (error) throw error

    // Jika berhasil
    isSuccess.value = true
    statusMessage.value = `Selesai! "${form.value.nama}" berhasil ditambahkan.`
    
    // Reset Form setelah sukses
    form.value = { nama: '', kategori: 'aktivitas', harga: null, deskripsi: '', gambar_url: '' }
  } catch (error) {
    isSuccess.value = false
    statusMessage.value = 'Gagal menyimpan: ' + error.message
  } finally {
    loading.value = false
  }
}
</script>