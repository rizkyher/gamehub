<script lang="ts">
    import { onMount } from 'svelte';
    import { fade } from 'svelte/transition';

    let { onComplete }: { onComplete: () => void } = $props();

    let progress = $state(0);
    let loadingText = $state("MENEMBUS HUJAN...");
    
    const phrases = [
        "MENCARI PAYUNG...",
        "MENYUSUN DUNIA...",
        "MEMUAT PIKSEL...",
        "SIAP BERTUALANG..."
    ];

    onMount(() => {
        let textIndex = 0;
        const textInterval = setInterval(() => {
            textIndex = (textIndex + 1) % phrases.length;
            loadingText = phrases[textIndex];
        }, 1000);

        const interval = setInterval(() => {
            const increment = Math.random() * 5; 
            progress = Math.min(progress + increment, 100);

            if (progress >= 100) {
                clearInterval(interval);
                clearInterval(textInterval);
                loadingText = "LET'S GO!";
                setTimeout(() => {
                    onComplete(); 
                }, 500);
            }
        }, 100);

        return () => {
            clearInterval(interval);
            clearInterval(textInterval);
        };
    });
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;700&family=VT323&display=swap" rel="stylesheet">
</svelte:head>

<div class="fixed inset-0 z-9999 flex flex-col items-center justify-center min-h-screen overflow-hidden font-pixel bg-white" out:fade={{ duration: 600 }}>
    
    <div class="absolute inset-0 bg-linear-to-b from-[#F9BA72]/40 via-[#41B78E]/30 to-white"></div>

    <div class="absolute inset-0 w-full h-full pointer-events-none overflow-hidden">
        
        <div class="absolute top-[5%] animate-cloud-slow scale-[2] opacity-80">
            <div class="pixel-cloud-shape"></div>
        </div>
        
        <div class="absolute top-[30%] animate-cloud-slow-left opacity-60 scale-[2.5] delay-1000 -scale-x-100">
            <div class="pixel-cloud-shape"></div>
        </div>
        
        <div class="absolute top-[50%] animate-cloud-medium scale-[2.2] opacity-90">
            <div class="pixel-cloud-shape"></div>
        </div>
        
        <div class="absolute bottom-[-5%] animate-cloud-fast-left scale-[3]">
             <div class="pixel-cloud-shape"></div>
        </div>


        <div class="pixel-rain-drop left-[5%] animate-rain-medium" style="animation-delay: 0.1s;"></div>
        <div class="pixel-rain-drop left-[12%] animate-rain-fast" style="animation-delay: 0.5s;"></div>
        <div class="pixel-rain-drop left-[20%] animate-rain-slow" style="animation-delay: 0.9s;"></div>
        <div class="pixel-rain-drop left-[28%] animate-rain-medium" style="animation-delay: 0.3s;"></div>
        <div class="pixel-rain-drop left-[35%] animate-rain-fast" style="animation-delay: 0.7s;"></div>
        <div class="pixel-rain-drop left-[42%] animate-rain-slow" style="animation-delay: 0.2s;"></div>
        <div class="pixel-rain-drop left-[50%] animate-rain-fast" style="animation-delay: 0.6s;"></div>
        <div class="pixel-rain-drop left-[58%] animate-rain-medium" style="animation-delay: 0.4s;"></div>
        <div class="pixel-rain-drop left-[65%] animate-rain-slow" style="animation-delay: 0.8s;"></div>
        <div class="pixel-rain-drop left-[73%] animate-rain-fast" style="animation-delay: 0.1s;"></div>
        <div class="pixel-rain-drop left-[80%] animate-rain-medium" style="animation-delay: 0.5s;"></div>
        <div class="pixel-rain-drop left-[88%] animate-rain-slow" style="animation-delay: 0.3s;"></div>
        <div class="pixel-rain-drop left-[95%] animate-rain-fast" style="animation-delay: 0.7s;"></div>
        

        <div class="absolute top-[30%] left-0 w-32 h-2 bg-[#F9BA72]/30 animate-wind-fast"></div>
        <div class="absolute bottom-[40%] left-0 w-48 h-2 bg-[#F9BA72]/20 animate-wind-medium" style="animation-delay: 0.5s"></div>

    </div>

    <div class="relative z-10 flex flex-col items-center justify-center w-full max-w-md px-6 gap-8">
        
        <div class="flex flex-col items-center animate-float relative">
            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-40 h-40 bg-[#F9BA72]/30 blur-2xl rounded-full"></div>
            
            <img 
                src="/logo.jpg" 
                alt="Khwarizmi Logo" 
                class="relative z-10 w-24 h-24 md:w-36 md:h-36 object-contain drop-shadow-xl"
            />
            
            <div class="mt-4 text-center relative z-10">
                <h1 class="text-4xl md:text-5xl font-black text-[#41B78E] tracking-widest drop-shadow-sm leading-none" style="text-shadow: 2px 2px 0px rgba(249, 186, 114, 0.5);">KHWARIZMI</h1>
                <div class="mt-2 flex justify-center gap-2">
                    <div class="w-2 h-2 bg-[#F9BA72]"></div>
                    <p class="text-sm font-bold text-[#F9BA72] tracking-[0.4em] uppercase bg-white/80 px-2 rounded">Spirit of Pixel</p>
                    <div class="w-2 h-2 bg-[#F9BA72]"></div>
                </div>
            </div>
        </div>

        <div class="w-full relative">
            <div class="flex justify-between text-[#41B78E] font-bold mb-2 text-sm md:text-base tracking-wider px-1">
                <span class="animate-pulse">{loadingText}</span>
                <span>{Math.floor(progress)}%</span>
            </div>
            
            <div class="w-full h-8 bg-white border-[3px] border-black p-1 shadow-[6px_6px_0_0_#F9BA72] rounded-sm overflow-hidden relative">
                <div 
                    class="h-full bg-[#41B78E] transition-all duration-200 ease-out relative overflow-hidden"
                    style="width: {progress}%"
                >
                    <div class="absolute inset-0 opacity-20 bg-[repeating-linear-gradient(45deg,transparent,transparent_10px,#000_10px,#000_20px)]"></div>
                    <div class="absolute inset-0 bg-[linear-gradient(90deg,transparent_0%,rgba(249,186,114,0.6)_50%,transparent_100%)] animate-shimmer w-[200%]"></div>
                </div>
            </div>
        </div>

    </div>
</div>

<style>
    .font-pixel {
        font-family: 'Pixelify Sans', 'VT323', monospace;
    }

    /* --- HUJAN PIKSEL (Teal) --- */
    .pixel-rain-drop {
        position: absolute; top: -50px; width: 3px; height: 15px; background-color: #41B78E; opacity: 0.8; box-shadow: 1px 1px 0 rgba(255,255,255,0.3);
    }
    @keyframes rainFall {
        0% { transform: translateY(0); opacity: 0.8; }
        100% { transform: translateY(110vh); opacity: 0.4; }
    }
    .animate-rain-fast { animation: rainFall 0.8s linear infinite; }
    .animate-rain-medium { animation: rainFall 1.2s linear infinite; }
    .animate-rain-slow { animation: rainFall 1.6s linear infinite; }

    /* --- BENTUK AWAN (Shadow diubah jadi Oranye) --- */
    .pixel-cloud-shape {
        position: relative; width: 160px; height: 50px; background-color: #ffffff; 
        /* Drop shadow oranye menggunakan rgba dari F9BA72 */
        filter: drop-shadow(4px 4px 0px rgba(249, 186, 114, 0.4)); 
    }
    .pixel-cloud-shape::before {
        content: ''; position: absolute; top: -25px; left: 25px; width: 70px; height: 35px; background: inherit;
    }
    .pixel-cloud-shape::after {
        content: ''; position: absolute; top: -15px; right: 25px; width: 50px; height: 25px; background: inherit;
    }

    /* --- ANIMASI --- */
    @keyframes float {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-12px); }
    }
    .animate-float { animation: float 3.5s ease-in-out infinite; }

    /* Awan Kanan */
    @keyframes cloudMoveRight {
        from { transform: translateX(-160%); }
        to { transform: translateX(160vw); }
    }
    .animate-cloud-slow { animation: cloudMoveRight 45s linear infinite; }
    .animate-cloud-medium { animation: cloudMoveRight 30s linear infinite; }
    .animate-cloud-fast { animation: cloudMoveRight 20s linear infinite; }

    /* Awan Kiri */
    @keyframes cloudMoveLeft {
        from { transform: translateX(160vw); }
        to { transform: translateX(-160%); }
    }
    .animate-cloud-slow-left { animation: cloudMoveLeft 50s linear infinite; }
    .animate-cloud-medium-left { animation: cloudMoveLeft 35s linear infinite; }
    .animate-cloud-fast-left { animation: cloudMoveLeft 22s linear infinite; }

    /* Angin */
    @keyframes windMove {
        from { left: -100px; opacity: 0; }
        50% { opacity: 1; }
        to { left: 100vw; opacity: 0; }
    }
    .animate-wind-fast { animation: windMove 3s linear infinite; }
    .animate-wind-medium { animation: windMove 5s linear infinite; }

    /* Shimmer */
    @keyframes shimmer {
        from { transform: translateX(-100%); }
        to { transform: translateX(50%); }
    }
    .animate-shimmer { animation: shimmer 1.5s infinite linear; }
</style>