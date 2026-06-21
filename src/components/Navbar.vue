<template>
  <nav class="bg-[#FAFAF8]/90 backdrop-blur-md sticky top-0 left-0 right-0 z-50 border-b border-gray-200/50 shadow-sm w-full">
    <div class="w-full px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16 items-center w-full">
        
        <div class="flex items-center gap-3">
          <button 
            @click="isMenuOpen = !isMenuOpen" 
            type="button"
            class="md:hidden p-2 rounded-md text-main-dark hover:bg-gray-100 transition-colors focus:outline-none"
            aria-label="Toggle Menu"
          >
            <svg 
              v-if="!isMenuOpen"
              class="h-6 w-6" 
              fill="none" 
              viewBox="0 0 24 24" 
              stroke="currentColor"
            >
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg 
              v-else
              class="h-6 w-6" 
              fill="none" 
              viewBox="0 0 24 24" 
              stroke="currentColor"
            >
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <div class="flex-shrink-0 flex items-center">
            <span class="brand-logo text-lg font-bold">pepepipi</span>
          </div>
        </div>
        
        <div class="flex items-center space-x-4 md:space-x-8">
          
          <div class="hidden md:flex space-x-8 items-center">
            <a href="#activities" class="text-main-dark hover:text-brand-blue font-medium transition-colors">Aktivitas</a>
            <a href="#hampers" class="text-main-dark hover:text-brand-blue font-medium transition-colors">Hampers</a>
            <a href="#simulator" class="text-main-dark hover:text-brand-blue font-medium transition-colors">Ide Aktivitas Anak</a>
          </div>
          
          <a 
            href="https://wa.me/6281218118138?text=Halo%20Pepepipi,%20saya%20tertarik%20tanya%20produknya!" 
            target="_blank"
            class="btn-primary-pastel rounded-full font-medium shadow-sm transition-all hover:scale-[1.02] flex items-center justify-center flex-shrink-0
                   h-10 w-10 p-0 md:h-auto md:w-auto md:px-5 md:py-2"
          >
            <svg 
              xmlns="http://www.w3.org/2000/svg" 
              viewBox="0 0 24 24" 
              fill="none" 
              stroke="currentColor" 
              stroke-width="2" 
              stroke-linecap="round" 
              stroke-linejoin="round" 
              class="w-5 h-5 flex-shrink-0"
            >
              <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/>
            </svg>
            <span class="hidden md:block ml-2">Hubungi Kami</span>
          </a>
          
        </div>

      </div>
    </div>

    <div 
      v-if="isMenuOpen" 
      class="md:hidden bg-[#FAFAF8] border-t border-gray-200/50 shadow-inner px-4 pt-2 pb-4 space-y-1"
    >
      <a 
        href="#activities" 
        @click="isMenuOpen = false"
        class="block px-3 py-2.5 rounded-md text-base font-medium text-main-dark hover:bg-gray-100 hover:text-brand-blue transition-colors"
      >
        Aktivitas
      </a>
      <a 
        href="#hampers" 
        @click="isMenuOpen = false"
        class="block px-3 py-2.5 rounded-md text-base font-medium text-main-dark hover:bg-gray-100 hover:text-brand-blue transition-colors"
      >
        Hampers
      </a>
      <a 
        href="#simulator" 
        @click="isMenuOpen = false"
        class="block px-3 py-2.5 rounded-md text-base font-medium text-main-dark hover:bg-gray-100 hover:text-brand-blue transition-colors"
      >
        Ide Aktivitas Anak
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue'

// State untuk mengontrol buka/tutup menu mobile
const isMenuOpen = ref(false)
</script>