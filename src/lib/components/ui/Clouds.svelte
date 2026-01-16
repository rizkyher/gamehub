<script lang="ts">
    // Mengubah semua warna menjadi Orange (#F9BA72) agar dominan
    const cloudLayers = [
        { top: '10%', duration: '45s', scale: '0.8', opacity: '0.9', delay: '0s', color: '#F9BA72' },
        { top: '20%', duration: '35s', scale: '1.3', opacity: '0.8', delay: '-8s', color: '#F9BA72' },
        { top: '40%', duration: '50s', scale: '1.0', opacity: '0.7', delay: '-15s', color: '#F9BA72' }, 
        { top: '65%', duration: '30s', scale: '1.6', opacity: '0.9', delay: '-25s', color: '#F9BA72' },
        { top: '85%', duration: '60s', scale: '0.9', opacity: '0.8', delay: '-10s', color: '#F9BA72' }
    ];
</script>

<div class="fixed inset-0 pointer-events-none overflow-hidden z-[-1]">
    {#each cloudLayers as cloud}
        <div 
            class="absolute -left-96 animate-drift"
            style="
                top: {cloud.top}; 
                animation-duration: {cloud.duration}; 
                animation-delay: {cloud.delay};
                transform: scale({cloud.scale});
                opacity: {cloud.opacity};
            "
        >
            <div class="relative w-40 h-16 bg-white border-2 border-transparent"
                 style="box-shadow: 12px 12px 0 0 {cloud.color}">
                
                <div class="absolute -top-8 left-8 w-16 h-16 bg-white"></div>
                <div class="absolute -top-5 left-20 w-20 h-12 bg-white"></div>
                
                <div class="absolute bottom-0 left-0 w-full h-4 opacity-100"
                     style="background-color: {cloud.color}"></div>
                
                <div class="absolute top-2 right-4 w-2 h-2 bg-slate-100"></div>
            </div>
        </div>
    {/each}
</div>

<style>
    @keyframes drift {
        from {
            transform: translateX(-25vw) scale(var(--scale, 1));
        }
        to {
            transform: translateX(120vw) scale(var(--scale, 1));
        }
    }

    .animate-drift {
        animation: drift linear infinite;
        will-change: transform;
    }
</style>