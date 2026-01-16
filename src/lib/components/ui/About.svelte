<script lang="ts">
    // Svelte 5 Props
    let { title = "Kisah Kami", story = "" } = $props();
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<section id="about" class="py-24 relative overflow-hidden font-pixel">
    <div class="max-w-6xl mx-auto px-6">
        <div class="flex flex-col lg:flex-row items-center gap-16">
            
            <div class="w-full lg:w-1/2 relative group">
                <div class="relative z-10 bg-white border-[3px] border-black p-3 
                            shadow-[12px_12px_0_0_#41B78E] transition-transform duration-500 group-hover:-translate-y-1">
                    
                    <div class="aspect-square bg-slate-50 border-[3px] border-black flex items-center justify-center overflow-hidden relative">
                        <div class="absolute inset-0 opacity-10" 
                             style="background-image: repeating-linear-gradient(45deg, #41B78E 0, #41B78E 2px, transparent 0, transparent 50%); background-size: 10px 10px;">
                        </div>
                        
                        <div class="relative scale-150 animate-bounce-slow">
                            <div class="w-20 h-20 bg-slate-900 border-4 border-black relative shadow-[4px_4px_0_0_#F9BA72]">
                                <div class="absolute top-5 left-3 w-3 h-3 bg-white border-2 border-black"></div>
                                <div class="absolute top-5 right-3 w-3 h-3 bg-white border-2 border-black"></div>
                                <div class="absolute bottom-4 left-1/2 -translate-x-1/2 w-8 h-2 bg-[#41B78E] border-2 border-black"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="absolute -top-6 -left-6 w-12 h-12 bg-[#F9BA72] border-[3px] border-black rotate-12 z-0 shadow-[4px_4px_0_0_#000]"></div>
                <div class="absolute -bottom-4 -right-4 w-10 h-10 bg-[#41B78E] border-[3px] border-black -rotate-12 z-20 shadow-[4px_4px_0_0_#000]"></div>
            </div>

            <div class="w-full lg:w-1/2 space-y-6">
                <div class="inline-block px-4 py-1 bg-black text-[#F9BA72] border-2 border-transparent text-xs font-bold uppercase tracking-[0.2em] shadow-[4px_4px_0_0_#41B78E]">
                    Our Journey
                </div>

                <div class="space-y-2">
                    <h2 class="text-4xl md:text-5xl font-bold text-slate-900 leading-tight">
                        Membangun <span class="text-[#41B78E] italic">Dunia Kecil</span> Lewat Piksel.
                    </h2>
                    <div class="h-3 w-32 bg-[#F9BA72] border-[3px] border-black"></div>
                </div>
                
                <div class="space-y-4 text-slate-700 leading-relaxed text-lg font-medium">
                    <p>
                        Berawal dari kekaguman terhadap estetika film-film Studio Ghibli yang hangat, kami memulai perjalanan untuk menciptakan game yang tidak hanya seru dimainkan, tapi juga menenangkan jiwa.
                    </p>
                    <p>
                        Setiap baris kode dan setiap kotak piksel yang kami susun bertujuan untuk membawa pemain ke dunia di mana imajinasi tidak memiliki batas. Kami percaya bahwa game adalah media bercerita yang paling kuat.
                    </p>
                </div>

                <div class="grid grid-cols-2 gap-4 pt-6">
                    <div class="p-4 border-[3px] border-black bg-white shadow-[6px_6px_0_0_#F9BA72] hover:translate-y-1 hover:shadow-[2px_2px_0_0_#F9BA72] transition-all">
                        <div class="text-3xl font-bold text-[#41B78E]">10+</div>
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-500">Game Rilis</div>
                    </div>
                    <div class="p-4 border-[3px] border-black bg-white shadow-[6px_6px_0_0_#41B78E] hover:translate-y-1 hover:shadow-[2px_2px_0_0_#41B78E] transition-all">
                        <div class="text-3xl font-bold text-[#F9BA72] text-shadow-black">100%</div>
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-500">Handcrafted</div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</section>

<style>
    /* Global Font Setting */
    .font-pixel {
        font-family: 'Pixelify Sans', sans-serif;
    }

    /* Text Shadow tipis untuk angka kuning agar terbaca di background putih */
    .text-shadow-black {
        text-shadow: 1px 1px 0px #000;
    }

    /* Animasi Mantul Lambat untuk Karakter */
    .animate-bounce-slow {
        animation: bounce 3s infinite;
    }

    @keyframes bounce {
        0%, 100% { transform: scale(1.5) translateY(-5%); }
        50% { transform: scale(1.5) translateY(5%); }
    }
</style>