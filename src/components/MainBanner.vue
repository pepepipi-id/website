<template>
  <section class="w-full bg-gradient-to-r from-[#FFF5EC] via-[#FFF0E0] to-[#FAFAF8] md:h-[500px] flex items-center border-b border-gray-100/50">
    
    <div class="w-full px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center md:h-[500px]">
        
        <div class="text-left order-2 md:order-1 z-10 py-6 md:py-0 w-full max-w-xl md:max-w-md lg:max-w-lg md:ml-auto pr-2 md:pr-6">        
          <h1 class="text-2xl sm:text-3xl lg:text-4xl font-black text-main-dark tracking-tight leading-snug mb-3">
            Temukan Ide Aktivitas Seru <br class="hidden sm:inline">
            dan Hampers Bermakna <br>
            <span class="text-brand-blue">untuk Anak</span>
          </h1>
          
          <p class="text-sm md:text-base text-main-muted mb-6 leading-relaxed">
            Ide bermain, aktivitas edukatif, dan hadiah spesial untuk menemani tumbuh kembang si kecil dengan atmosfer yang hangat dan penuh kasih sayang.
          </p>
          
          <div class="flex flex-wrap gap-3">
            <a href="#simulator" class="btn-primary-pastel px-5 py-2.5 rounded-full text-sm font-semibold shadow-sm transition-all hover:scale-[1.02]">
              Cari Ide Aktivitas Anak
            </a>
            <a href="#hampers" class="bg-white text-main-dark border border-[#FED7B7] px-5 py-2.5 rounded-full text-sm font-medium hover:bg-[#FFFDF9] transition-all shadow-sm">
              Lihat Hampers
            </a>
          </div>
        </div>

        <div class="order-1 md:order-2 w-full h-full flex justify-center md:justify-start items-center relative">
          <div class="relative w-full max-w-xl md:max-w-none h-[240px] sm:h-[320px] md:h-full rounded-2xl md:rounded-none overflow-hidden shadow-sm md:shadow-none">
            
            <img 
              src="../assets/hero-banner.png" 
              alt="Temukan Aktivitas Seru Pepepipi bersama Anak" 
              class="w-full h-full object-cover object-center md:object-right"
            />

            <div class="absolute inset-y-0 left-0 w-1/4 bg-gradient-to-r from-[#FFF0E0] via-[#FFF0E0]/30 to-transparent hidden md:block"></div>
            <div class="absolute inset-x-0 bottom-0 h-1/5 bg-gradient-to-t from-[#FFF0E0] via-[#FFF0E0]/20 to-transparent hidden md:block"></div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>