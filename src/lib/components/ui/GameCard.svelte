<script lang="ts">
    import { fade } from 'svelte/transition';

    // 1. Update Interface: Tambah 'playUrl'
    interface GameItem {
        id: number;
        title: string;
        desc: string;
        tags: string[];
        image: string;
        playUrl: string; // <--- Property baru untuk Link Game
    }

    // Menerima props game
    let { game }: { game: GameItem } = $props();
    
    let isHovered = $state(false);
    let isModalOpen = $state(false);

    const toggleModal = () => {
        isModalOpen = !isModalOpen;
        if (typeof document !== 'undefined') {
            document.body.style.overflow = isModalOpen ? 'hidden' : 'auto';
        }
    };
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<div class="snap-center shrink-0 w-70 md:w-87.5 py-4 font-pixel" role="presentation">
    <div 
        role="button"
        tabindex="0"
        onmouseenter={() => isHovered = true}
        onmouseleave={() => isHovered = false}
        onclick={toggleModal}
        onkeydown={(e) => e.key === 'Enter' && toggleModal()}
        class="group relative bg-white border-[3px] border-black p-2 transition-all duration-300 
               cursor-pointer outline-none
               {isHovered ? '-translate-y-2 shadow-[8px_8px_0_0_#F9BA72]' : 'shadow-[6px_6px_0_0_#000]'}"
    >
        <div class="aspect-video border-[3px] border-black relative overflow-hidden bg-slate-200">
            <img 
                src={game.image} 
                alt={game.title}
                class="w-full h-full object-cover transition-transform duration-500 {isHovered ? 'scale-110 rotate-1' : 'scale-100'}"
            />
            
            {#if isHovered}
                <div transition:fade={{duration: 100}} class="absolute inset-0 bg-[#F9BA72]/90 flex items-center justify-center backdrop-blur-[2px] z-10">
                    <span class="bg-white border-[3px] border-black px-4 py-2 font-bold shadow-[4px_4px_0_0_#000] -rotate-3 text-black text-sm tracking-widest">
                        VIEW DETAIL
                    </span>
                </div>
            {/if}
        </div>

        <div class="p-4 bg-white transition-colors border-t-0 {isHovered ? 'bg-slate-50' : ''}">
            <h2 class="text-2xl font-bold text-slate-900 uppercase mb-3 leading-none group-hover:text-[#41B78E] transition-colors truncate">
                {game.title}
            </h2>
            <div class="flex gap-2 flex-wrap">
                {#each game.tags as tag}
                    <span class="bg-white border-2 border-black px-2 py-1 text-[10px] font-bold uppercase shadow-[2px_2px_0_0_#41B78E] text-slate-700">
                        {tag}
                    </span>
                {/each}
            </div>
        </div>
    </div>
</div>

{#if isModalOpen}
    <div 
        role="button"
        tabindex="-1" 
        class="fixed inset-0 bg-slate-900/80 backdrop-blur-md z-100 flex items-center justify-center p-4 md:p-6 cursor-default font-pixel"
        onclick={toggleModal}
        onkeydown={(e) => e.key === 'Escape' && toggleModal()}
        transition:fade={{ duration: 150 }}
    >
        <div 
            role="dialog"
            aria-modal="true"
            tabindex="0"
            class="bg-white border-4 border-black w-full max-w-4xl shadow-[12px_12px_0_0_#000] overflow-hidden animate-pop cursor-default outline-none relative"
            onclick={(e) => e.stopPropagation()}
            onkeydown={(e) => e.stopPropagation()}
        >
            <div class="bg-[#41B78E] border-b-4 border-black p-4 flex justify-between items-center text-white relative">
                <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#000_2px,transparent_0)] bg-size-[6px_6px]"></div>
                <h2 class="text-2xl md:text-3xl font-bold uppercase tracking-wide relative z-10 text-shadow-sm">Game Details</h2>
                <button 
                    onclick={toggleModal} 
                    class="text-4xl leading-none hover:text-[#F9BA72] font-bold transition-colors focus:outline-none relative z-10 active:scale-90"
                    aria-label="Close Modal"
                >
                    ×
                </button>
            </div>

            <div class="p-6 md:p-8 flex flex-col md:flex-row gap-8">
                <div class="w-full md:w-1/2 aspect-video md:aspect-square border-4 border-black relative shadow-[8px_8px_0_0_#000] overflow-hidden bg-slate-200">
                     <img 
                        src={game.image} 
                        alt={game.title}
                        class="w-full h-full object-cover"
                    />
                </div>

                <div class="w-full md:w-1/2 flex flex-col">
                    <div class="space-y-2 mb-4">
                        <h3 class="text-4xl font-bold uppercase text-slate-900 leading-tight">
                            {game.title}
                        </h3>
                        <div class="h-2 w-24 bg-[#F9BA72] border-2 border-black"></div>
                    </div>
                    
                    <div class="flex gap-2 flex-wrap mb-6">
                        {#each game.tags as tag}
                            <span class="bg-black text-[#F9BA72] border border-black text-xs px-3 py-1 font-bold uppercase tracking-widest">
                                {tag}
                            </span>
                        {/each}
                    </div>

                    <p class="text-slate-700 text-lg leading-relaxed border-l-[6px] border-[#41B78E] pl-4 py-2 mb-8 grow">
                        {game.desc}
                    </p>

                    <a 
                        href={game.playUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="block text-center no-underline w-full py-4 bg-[#41B78E] text-white font-bold text-xl uppercase tracking-widest border-[3px] border-black 
                               shadow-[6px_6px_0_0_#000] 
                               hover:bg-[#F9BA72] hover:text-black hover:shadow-[3px_3px_0_0_#000] hover:translate-x-0.5 hover:translate-y-0.5
                               active:translate-x-1 active:translate-y-1 active:shadow-none transition-all outline-none"
                    >
                        PLAY NOW
                    </a>
                </div>
            </div>
        </div>
    </div>
{/if}

<style>
    .font-pixel {
        font-family: 'Pixelify Sans', sans-serif;
    }

    .text-shadow-sm {
        text-shadow: 2px 2px 0px rgba(0,0,0,0.2);
    }

    .animate-pop {
        animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    @keyframes popIn {
        from { opacity: 0; transform: scale(0.9) translateY(20px); }
        to { opacity: 1; transform: scale(1) translateY(0); }
    }
</style>