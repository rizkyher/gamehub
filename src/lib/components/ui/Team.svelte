<script lang="ts">
    import { onMount } from 'svelte';

    interface Member {
        name: string;
        role: string;
        avatarColor: string;
        bio: string;
        photoUrl?: string; 
    }

    let { members }: { members: Member[] } = $props();

    let isVisible = $state(false);
    let sectionRef: HTMLElement;
    
    // State untuk melacak kartu yang sedang terbuka
    let flippedCards = $state(new Set<number>());

    function toggleFlip(index: number) {
        const newFlipped = new Set(flippedCards);
        if (newFlipped.has(index)) {
            newFlipped.delete(index);
        } else {
            newFlipped.add(index);
        }
        flippedCards = newFlipped;
    }

    function handleKeydown(e: KeyboardEvent, index: number) {
        if (e.key === 'Enter' || e.key === ' ') {
            e.preventDefault();
            toggleFlip(index);
        }
    }

    onMount(() => {
        const observer = new IntersectionObserver((entries) => {
            if (entries[0].isIntersecting) {
                isVisible = true;
                observer.disconnect();
            }
        }, { threshold: 0.1 });

        if (sectionRef) observer.observe(sectionRef);

        return () => observer.disconnect();
    });
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<section id="team" class="py-24 font-pixel overflow-hidden" bind:this={sectionRef}>
    <div class="max-w-6xl mx-auto px-6">
        
        <div class="flex flex-col md:flex-row justify-between items-end mb-12 relative">
            <div class="text-left">
                <div class="absolute -top-10 left-0 text-4xl animate-bounce delay-700 opacity-60">👾</div>
                
                <h2 class="text-5xl md:text-6xl font-bold text-slate-900 uppercase tracking-wide inline-block relative z-10">
                    The Creators
                    <div class="absolute -bottom-2 left-0 w-full h-2 bg-[#F9BA72] border-2 border-black shadow-[3px_3px_0_0_#000]"></div>
                </h2>
                <p class="mt-6 text-slate-600 text-lg max-w-xl">
                    Klik kartu untuk melihat wujud asli kami.
                </p>
            </div>

            <div class="hidden md:block text-xs font-bold bg-black text-[#F9BA72] px-4 py-2 border-2 border-transparent shadow-[4px_4px_0_0_#41B78E] uppercase tracking-wider animate-pulse mb-2">
                Shift + Scroll →
            </div>
        </div>

        <div class="flex overflow-x-auto gap-8 pb-16 pt-4 px-2 no-scrollbar snap-x snap-mandatory scroll-smooth">
            {#each members as member, i}
                <div 
                    class="group relative h-112.5 min-w-75 md:min-w-85 cursor-pointer 
                           opacity-0 translate-y-10 transition-all duration-300 snap-center"
                    class:animate-entry={isVisible}
                    style="animation-delay: {i * 150}ms; animation-fill-mode: forwards; perspective: 1000px;"
                >
                    <div 
                        role="button"
                        tabindex="0"
                        onkeydown={(e) => handleKeydown(e, i)}
                        onclick={() => toggleFlip(i)}
                        class="relative w-full h-full transition-transform duration-700 preserve-3d shadow-[10px_10px_0_0_#F9BA72] group-hover:shadow-[6px_6px_0_0_#41B78E] border-[3px] border-black"
                        class:rotate-y-180={flippedCards.has(i)}
                    >

                        <div class="absolute inset-0 backface-hidden bg-white p-6 flex flex-col justify-between z-20">
                            <div class="w-full aspect-square {member.avatarColor} border-[3px] border-black mb-4 relative overflow-hidden flex items-center justify-center group-hover:bg-[#f0fdf4] transition-colors">
                                <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#000_2px,transparent_0)] bg-size-[8px_8px]"></div>
                                
                                <div class="relative scale-[2.5]">
                                    <div class="w-12 h-12 bg-white border-2 border-black shadow-[2px_2px_0_0_rgba(0,0,0,0.1)] relative">
                                        <div class="absolute top-4 left-2 w-2 h-2 bg-black animate-blink"></div>
                                        <div class="absolute top-4 right-2 w-2 h-2 bg-black animate-blink"></div>
                                        <div class="absolute top-6 left-1 w-2 h-1 bg-[#F9BA72] opacity-60"></div>
                                        <div class="absolute top-6 right-1 w-2 h-1 bg-[#F9BA72] opacity-60"></div>
                                        <div class="absolute bottom-3 left-1/2 -translate-x-1/2 w-4 h-1 bg-black group-hover:w-2 group-hover:h-2 group-hover:rounded-full transition-all"></div>
                                    </div>
                                </div>

                                <div class="absolute top-3 right-3 bg-black text-[#F9BA72] text-[10px] font-bold px-2 py-1 border border-white/20 shadow-sm animate-pulse">
                                    FLIP ↻
                                </div>
                            </div>

                            <div class="text-center grow flex flex-col justify-center">
                                <h3 class="text-3xl font-bold uppercase text-slate-900 mb-1 leading-none">{member.name}</h3>
                                <div class="flex justify-center mb-4">
                                    <span class="text-[#41B78E] font-bold text-xs tracking-[0.2em] uppercase border-b-2 border-slate-100 pb-2">
                                        {member.role}
                                    </span>
                                </div>
                                <p class="text-slate-600 text-sm italic leading-relaxed">
                                    "{member.bio}"
                                </p>
                            </div>

                            <div class="flex justify-center gap-3 mt-4 border-t-2 border-dashed border-slate-200 pt-4">
                                <div class="w-8 h-8 bg-slate-100 border-2 border-black flex items-center justify-center">GH</div>
                                <div class="w-8 h-8 bg-slate-100 border-2 border-black flex items-center justify-center">TW</div>
                            </div>
                        </div>

                        <div class="absolute inset-0 backface-hidden rotate-y-180 bg-slate-900 border-[3px] border-black overflow-hidden z-10">
                            <div class="relative w-full h-full group/back">
                                <img 
                                    src={member.photoUrl || `https://i.pravatar.cc/500?u=${member.name}`} 
                                    alt={member.name} 
                                    class="w-full h-full object-cover filter grayscale group-hover/back:grayscale-0 transition-all duration-700"
                                />
                                
                                <div class="absolute inset-0 bg-linear-to-t from-black via-black/40 to-transparent opacity-90"></div>
                                <div class="absolute inset-0 opacity-20 pointer-events-none" style="background-image: radial-gradient(rgba(0,0,0,0) 1px, transparent 1px); background-size: 4px 4px; background-color: rgba(0, 0, 0, 0.1);"></div>

                                <div class="absolute bottom-0 left-0 w-full p-6 text-center">
                                    <div class="inline-block bg-[#F9BA72] text-black border-2 border-black px-3 py-1 mb-3 transform -rotate-1 shadow-[4px_4px_0_0_#000]">
                                        <span class="text-[10px] font-bold uppercase tracking-widest">Real Life Mode</span>
                                    </div>
                                    <h3 class="text-4xl font-bold text-white uppercase tracking-wider drop-shadow-md">
                                        {member.name}
                                    </h3>
                                    <p class="text-slate-300 text-xs uppercase tracking-[0.3em] mt-2 border-t border-slate-600 pt-2 inline-block">
                                        {member.role}
                                    </p>
                                </div>

                                <button 
                                    aria-label="Close"
                                    class="absolute top-4 right-4 w-10 h-10 bg-white border-[3px] border-black flex items-center justify-center text-black hover:bg-rose-500 hover:text-white transition-colors shadow-[4px_4px_0_0_#000] active:translate-y-1 active:shadow-none"
                                >
                                    ✕
                                </button>
                            </div>
                        </div>

                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>

<style>
    .font-pixel { font-family: 'Pixelify Sans', sans-serif; }

    /* 3D Transform */
    .preserve-3d { transform-style: preserve-3d; }
    .backface-hidden { backface-visibility: hidden; -webkit-backface-visibility: hidden; }
    .rotate-y-180 { transform: rotateY(180deg); }

    /* Animations */
    .animate-entry { animation: fadeInUp 0.6s cubic-bezier(0.2, 0.8, 0.2, 1) forwards; }
    @keyframes fadeInUp {
        from { opacity: 0; transform: translateY(40px); }
        to { opacity: 1; transform: translateY(0); }
    }

    .animate-blink { animation: blink 4s infinite; }
    @keyframes blink {
        0%, 96%, 100% { height: 8px; transform: scaleY(1); }
        98% { height: 2px; transform: scaleY(0.1); }
    }

    /* Scrollbar Hidden Helper */
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
</style>