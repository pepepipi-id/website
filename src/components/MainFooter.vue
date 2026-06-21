<template>
  <!-- Menggunakan bg-warm-light agar kontras dengan body bg-base-warm, dan border atas yang soft -->
  <footer class="bg-warm-light border-t border-slate-100 py-16 mt-20 text-left text-main-dark">
    <div class="max-w-6xl mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-12 mb-12">
        
        <!-- KOLOM 1: BRANDING & SOSMED/MARKETPLACE BERWARNA -->
        <div class="flex flex-col space-y-6">
          <!-- Memakai utility class .brand-logo yang sudah Anda buat, diperbesar ke text-4xl -->
          <h2 class="brand-logo text-4xl tracking-tight">pepepipi</h2>
          <p class="text-main-muted text-sm max-w-xs leading-relaxed">
            Teman belanja Hampers dan Alat tulis anak. Dengan produk dan hampers pilihan terbaik demi kebahagiaan dan tumbuh kembang keluarga Anda.
          </p>
          
          <!-- Ikon murni berwarna asli tanpa teks label -->
          <div class="flex items-center gap-5">
            <!-- Instagram -->
            <a href="https://instagram.com/pepepipi.id" target="_blank" class="transition-all transform hover:scale-110 block">
              <img src="../assets/logo-instagram.png" alt="Instagram Pepepipi" class="w-6 h-6 object-contain" />
            </a>
            <!-- TikTok -->
            <a href="https://tiktok.com/@pepepipi.id" target="_blank" class="transition-all transform hover:scale-110 block">
              <img src="../assets/logo-tiktok.png" alt="TikTok Pepepipi" class="w-6 h-6 object-contain" />
            </a>
            <!-- Tokopedia -->
            <a href="https://tokopedia.com/pepepipi" target="_blank" class="transition-all transform hover:scale-110 block">
              <img src="../assets/logo-tokopedia.png" alt="Tokopedia Pepepipi" class="w-6 h-6 object-contain" />
            </a>
            <!-- Shopee -->
            <a href="https://shopee.co.id/pepepipi" target="_blank" class="transition-all transform hover:scale-110 block">
              <img src="../assets/logo-shopee.png" alt="Shopee Pepepipi" class="w-6 h-6 object-contain" />
            </a>
          </div>
        </div>

        <!-- KOLOM 2: TENTANG KAMI -->
        <div class="flex flex-col space-y-4">
          <h3 class="text-xs font-bold uppercase tracking-widest text-main-dark opacity-80"><br>Tentang Kami</h3>
          <p class="text-main-muted text-sm leading-relaxed">
            Sejak tahun 2019, Pepepipi hadir dengan berbagai alat tulis anak dan hampers pilihan.<br>Kami ingin menjadi teman yang terbaik bagi pada ibu dalam proses tumbuh kembang anak tercinta. Menciptakan momen seru, interaktif, dan edukatif bersama si kecil. 
          </p>
        </div>

        <!-- KOLOM 3: KONTAK KAMI -->
        <div class="flex flex-col space-y-4">
          <h3 class="text-xs font-bold uppercase tracking-widest text-main-dark opacity-80"><br>Kontak Kami</h3>
          <ul class="text-main-muted text-sm space-y-3">
            <li class="flex items-start gap-3">
              <span class="font-bold text-main-dark min-w-[80px]">Jam Buka:</span>
              <span>Senin - Jumat <br> 09.00 - 16.30 WIB<br>Sabtu <br> 09.00-12.00</span>
            </li>
            <li class="flex items-center gap-3">
              <span class="font-bold text-main-dark min-w-[80px]">WhatsApp:</span>
              <a href="https://wa.me/6281218118138" target="_blank" class="hover:text-main-dark transition-colors underline decoration-dotted">+62 812-181 181 38</a>
            </li>
            <li class="flex items-start gap-3">
              <span class="font-bold text-main-dark min-w-[80px]">Alamat:</span>
              <span>Taman Kaliandra no 26, Bandung, Jawa Barat, Indonesia</span>
            </li>
          </ul>
        </div>
      </div>

      <!-- BAGIAN BAWAH (COPYRIGHT & PRIVASI) -->
      <div class="border-t border-stone-200/60 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
        <p class="text-xs text-main-muted">&copy; 2019 pepepipi. All rights reserved.</p>
        <div class="flex gap-6 text-xs text-main-muted">
          <a href="javascript:void(0)" class="hover:text-main-dark transition-colors">Privacy Policy</a>
          <a href="javascript:void(0)" class="hover:text-main-dark transition-colors">Terms of Service</a>
        </div>
      </div>
    </div>
  </footer>
</template>