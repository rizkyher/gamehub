<script lang="ts">
    interface Props {
        title: string;
        subtitle: string;
    }

    let { title, subtitle }: Props = $props();

    // Memecah judul menjadi array karakter agar bisa dianimasikan satu per satu
    let letters = $derived(title.split(''));
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<header class="text-center mb-20 mt-16 px-4">
    <div class="inline-block relative group cursor-default">
        
        <h1 class="flex justify-center text-6xl md:text-8xl font-bold text-slate-900 mb-6 tracking-wide uppercase z-10 relative">
            {#each letters as letter, i}
                <span class="pixel-wave inline-block hover:text-[#41B78E] transition-colors duration-200"
                      style="animation-delay: {i * 100}ms">
                    {@html letter === ' ' ? '&nbsp;' : letter}
                </span>
            {/each}
        </h1>

        <div class="h-3 w-full bg-[#F9BA72] border-[3px] border-black absolute -bottom-2 left-0 
                    shadow-[5px_5px_0_0_#000] transition-all duration-300
                    group-hover:translate-x-1 group-hover:translate-y-1 group-hover:shadow-none
                    group-hover:bg-[#41B78E]">
        </div>
    </div>

    <p class="mt-8 text-slate-600 text-lg md:text-xl font-medium tracking-wide max-w-2xl mx-auto leading-relaxed">
        {subtitle}
    </p>
</header>

<style>
    header {
        font-family: 'Pixelify Sans', sans-serif;
    }

    /* Definisi Animasi Gelombang */
    .pixel-wave {
        /* ease-in-out memberikan kesan mengapung yang halus */
        animation: float-text 3s ease-in-out infinite;
    }

    @keyframes float-text {
        0%, 100% {
            transform: translateY(0);
            color: #0f172a; /* Slate-900 (Hitam default) */
        }
        50% {
            transform: translateY(-12px); /* Naik ke atas */
            /* PERUBAHAN: Warna puncak jadi Orange (#F9BA72) */
            color: #F9BA72; 
            text-shadow: 3px 3px 0px #000; /* Menambah shadow saat naik */
        }
    }
</style>