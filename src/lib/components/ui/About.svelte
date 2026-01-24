<script lang="ts">
    // Svelte 5 Props
    let { title = "Ayo Main", story = "" } = $props();
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<section id="play" class="py-24 relative overflow-hidden font-pixel">
    <div class="max-w-6xl mx-auto px-6">
        <div class="flex flex-col lg:flex-row items-center gap-16">
            
            <div class="w-full lg:w-1/2 flex justify-center">
                <img 
                    src="logo.jpg" 
                    alt="Preview Game Pixel Art"
                    class="w-full max-w-sm h-auto rounded-sm border-[3px] border-black shadow-[8px_8px_0_0_#000] hover:-translate-y-1 hover:shadow-[12px_12px_0_0_#41B78E] transition-all duration-300"
                />
            </div>

            <div class="w-full lg:w-1/2 space-y-6">
                <div class="inline-block px-4 py-1 bg-black text-[#F9BA72] border-2 border-transparent text-xs font-bold uppercase tracking-[0.2em] shadow-[4px_4px_0_0_#41B78E]">
                    Level Up Now
                </div>

                <div class="space-y-2">
                    <h2 class="text-4xl md:text-5xl font-bold text-slate-900 leading-tight">
                        Rasakan Serunya <span class="text-[#41B78E] italic">Game</span> Buatan Kami.
                    </h2>
                    <div class="h-3 w-32 bg-[#F9BA72] border-[3px] border-black"></div>
                </div>
                
                <div class="space-y-4 text-slate-700 leading-relaxed text-lg font-medium">
                    <p>
                        Jangan biarkan waktu luangmu membosankan! Kami menghadirkan koleksi game unik yang siap menguji ketangkasan, strategi, dan imajinasimu.
                    </p>
                    <p>
                        Dari petualangan yang menantang hingga teka-teki yang mengasah otak, semua dirancang khusus untuk memberikan pengalaman bermain yang tak terlupakan. Pilih gamemu dan raih skor tertinggi sekarang juga!
                    </p>
                </div>

                <div class="grid grid-cols-2 gap-4 pt-6">
                    <button class="text-left w-full p-4 border-[3px] border-black bg-white shadow-[6px_6px_0_0_#F9BA72] hover:translate-y-1 hover:shadow-[2px_2px_0_0_#F9BA72] transition-all group">
                        <div class="text-3xl font-bold text-[#41B78E] group-hover:underline">MAIN</div>
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-500">Sekarang Juga</div>
                    </button>
                    
                    <div class="p-4 border-[3px] border-black bg-white shadow-[6px_6px_0_0_#41B78E] hover:translate-y-1 hover:shadow-[2px_2px_0_0_#41B78E] transition-all">
                        <div class="text-3xl font-bold text-[#F9BA72] text-shadow-black">GRATIS</div>
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-500">Akses Penuh</div>
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
</style>