<script lang="ts">
    // Props untuk fleksibilitas
    let { 
        videoSrc = "vario.mp4", 
        title = "Unknown Game" 
    } = $props();

    let videoRef: HTMLVideoElement;
    let isMuted = $state(true);
    let isPlaying = $state(true);

    function toggleMute() {
        if (!videoRef) return;
        videoRef.muted = !videoRef.muted;
        isMuted = videoRef.muted;
    }

    function togglePlay() {
        if (!videoRef) return;
        if (videoRef.paused) {
            videoRef.play();
            isPlaying = true;
        } else {
            videoRef.pause();
            isPlaying = false;
        }
    }
</script>

<div class="relative w-full max-w-4xl mx-auto group font-pixel select-none">
    
    <div class="absolute -top-4 -right-4 z-20 bg-[#F9BA72] border-[3px] border-black px-4 py-1 
                font-bold uppercase text-xs shadow-[4px_4px_0_0_#000] rotate-3 animate-pulse">
        Now Playing
    </div>

    <div class="bg-[#41B78E] p-4 pb-10 rounded-t-2xl rounded-b-lg border-[6px] border-black 
                shadow-[12px_12px_0_0_rgba(0,0,0,0.2)] relative transition-transform hover:-translate-y-1">
        
        <div class="bg-black aspect-video w-full border-4 border-black relative rounded-sm overflow-hidden group/screen">
            
            <video 
                bind:this={videoRef}
                src={videoSrc}
                autoplay 
                muted 
                loop 
                playsinline
                class="w-full h-full object-cover opacity-80 group-hover/screen:opacity-100 transition-opacity duration-500"
            ></video>

            <div class="pointer-events-none absolute inset-0 z-10 
                        bg-[linear-gradient(rgba(18,16,16,0)_50%,rgba(0,0,0,0.2)_50%),linear-gradient(90deg,rgba(255,0,0,0.06),rgba(0,255,0,0.02),rgba(0,0,255,0.06))] 
                        bg-size-[100%_4px,3px_100%]">
            </div>

            <div class="absolute inset-0 bg-linear-to-tr from-transparent via-white/5 to-white/10 pointer-events-none z-10"></div>

            <div class="absolute inset-0 flex items-center justify-center gap-6 z-20 opacity-0 group-hover/screen:opacity-100 transition-opacity duration-300 bg-black/20 backdrop-blur-[2px]">
                
                <button 
                    onclick={togglePlay}
                    class="w-14 h-14 bg-[#F9BA72] border-[3px] border-black flex items-center justify-center
                           shadow-[4px_4px_0_0_#000] hover:translate-x-1 hover:translate-y-1 hover:shadow-none hover:bg-white transition-all"
                    aria-label={isPlaying ? "Pause" : "Play"}
                >
                    {#if isPlaying}
                        <div class="flex gap-1.5">
                            <div class="w-2 h-6 bg-black"></div>
                            <div class="w-2 h-6 bg-black"></div>
                        </div>
                    {:else}
                        <div class="w-0 h-0 border-l-16 border-l-black border-y-10 border-y-transparent ml-1"></div>
                    {/if}
                </button>

                <button 
                    onclick={toggleMute}
                    class="w-14 h-14 bg-[#41B78E] border-[3px] border-black flex items-center justify-center
                           shadow-[4px_4px_0_0_#000] hover:translate-x-1 hover:translate-y-1 hover:shadow-none hover:bg-white transition-all"
                    aria-label={isMuted ? "Unmute" : "Mute"}
                >
                    <span class="text-2xl font-bold text-black">
                        {isMuted ? '🔇' : '🔊'}
                    </span>
                </button>

            </div>
        </div>

        <div class="mt-4 flex justify-between items-end px-2">
            <div class="flex flex-col">
                <span class="text-[10px] uppercase font-bold text-[#1f5642] tracking-widest mb-1">System Ready</span>
                <div class="bg-black/10 px-3 py-1 border-2 border-black/20 rounded-sm">
                    <span class="text-xs font-bold uppercase tracking-wider text-[#0f2e22]">{title}</span>
                </div>
            </div>

            <div class="flex items-center gap-4">
                <div class="flex gap-1">
                    {#each Array(4) as _}
                        <div class="w-1 h-3 bg-black/20 rounded-full"></div>
                    {/each}
                </div>
                <div class="relative w-3 h-3">
                    <div class="absolute inset-0 bg-red-500 rounded-full animate-ping opacity-75"></div>
                    <div class="relative w-3 h-3 bg-red-600 rounded-full border border-black/30"></div>
                </div>
            </div>
        </div>
    </div>

    <div class="w-1/3 h-6 bg-[#2d8a68] mx-auto border-x-[6px] border-black relative z-0"></div>
    <div class="w-1/2 h-4 bg-[#2d8a68] mx-auto border-[6px] border-black rounded-b-xl shadow-[0_8px_0_rgba(0,0,0,0.1)] relative z-0"></div>

</div>

<style>
    .font-pixel {
        font-family: 'Pixelify Sans', sans-serif;
    }
</style>