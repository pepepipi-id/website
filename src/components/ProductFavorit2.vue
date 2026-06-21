    <template>
    <section id="hampers" class="max-w-6xl mx-auto px-4 py-12">
        <div class="mb-8">
        <h2 class="text-2xl font-black text-[#1e293b] tracking-tight">
            Hampers Terfavorit Pilihan Bunda
        </h2>
        <p class="text-xs font-semibold text-[#64748b] uppercase tracking-wider mt-1">
            ✨ Bingkisan Premium untuk Momen Spesial
        </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div 
            v-for="item in products" 
            :key="item.id" 
            class="bg-[#FFF4EA] border border-[#FFC89A] rounded-2xl p-5 shadow-xs hover:shadow-md transition-all duration-200 transform hover:-translate-y-1 flex flex-col justify-between"
        >
            <div>
            <div class="w-full aspect-[1/1] bg-white rounded-xl overflow-hidden mb-4 border border-[#FFC89A]/40">
                <img :src="item.foto_url" class="w-full h-full object-cover" :alt="item.nama_produk">
            </div>
            
            <div class="flex items-center justify-between gap-2 mb-2">
                <span class="text-[12px] px-2 py-0.5 rounded-full bg-orange-100 text-orange-600 font-semibold">
                🔥 Terjual : {{(Number(item.label_terjual) || 0).toLocaleString('id-ID')}} +
                </span>
                <span class="text-[12px] font-bold text-[#d97706]">
                Rp {{ item.harga.toLocaleString('id-ID') }}
                </span>
            </div>
            <h3 class="font-bold text-base text-[#1e293b] mb-4 leading-snug">
                {{ item.nama_produk }}
            </h3>
            </div>

            <a 
            :href="'https://wa.me/6281218118138?text=' + encodeURIComponent('Halo Pepepipi, saya tertarik untuk memesan produk Hampers:  ' + item.nama_produk + ' yang ada di website.')"
            target="_blank"
            class="block w-full text-center bg-[#5CA7D4] text-white text-s font-bold py-3 rounded-xl hover:bg-[#4188b2] transition-all"
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
    // Ambil maksimal 3 data hampers terlaris
    const { data } = await supabase
        .from('products')
        .select('*')
        .eq('kategori', 'Hampers')
        .eq('is_active', true)
        .limit(3)
    console.log(products.value)
    
    // Jika database kosong, kita kasih data contoh (mock) bertema pastel
    products.value = data && data.length > 0 ? data : [
        { id: 1, nama_produk: "Hampers Custom Baby Born Box (Pastel Edition)", harga: 249000, foto_url: "https://images.unsplash.com/photo-1549465220-1a8b9238cd48?w=500", label_terjual: "Terjual 1.5 Juta++" },
        { id: 2, nama_produk: "Premium Kids Birthday Gift Set A", harga: 175000, foto_url: "https://images.unsplash.com/photo-1513201099705-a9746e1e201f?w=500", label_terjual: "Terjual 800++" },
        { id: 3, nama_produk: "Paket Hampers Hari Raya & Syukuran Keluarga", harga: 320000, foto_url: "https://images.unsplash.com/photo-1549465220-1a8b9238cd48?w=500", label_terjual: "Terjual 2.1 Juta++" }
    ]
    })
    </script>