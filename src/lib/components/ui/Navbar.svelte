<script lang="ts">
    import { slide } from 'svelte/transition';
    import { cubicOut } from 'svelte/easing';

    // --- Svelte 5 State Management ---
    let scrollY = $state(0);
    let isMenuOpen = $state(false);

    // Derived state: Navbar mengecil saat di-scroll
    let isScrolled = $derived(scrollY > 20);

    // Data Navigasi
    const navLinks = [
        { name: 'Home', href: '#' },
        { name: 'Games', href: '#games' },
        { name: 'Team', href: '#team' },
        { name: 'About', href: '#about' }
    ];

    function toggleMenu() {
        isMenuOpen = !isMenuOpen;
    }
</script>

<svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous">
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<svelte:window bind:scrollY={scrollY} />

<nav class="fixed top-0 left-0 w-full z-50 transition-all duration-300 ease-out px-4 md:px-6 
    {isScrolled ? 'py-2' : 'py-4 md:py-6'}">
    
    <div class="max-w-7xl mx-auto">
        <div class="relative bg-white border-[3px] border-black shadow-[6px_6px_0_0_#000] 
                    transition-all duration-300 flex flex-col">
            
            <div class="flex justify-between items-center p-3 md:px-6 md:py-4 bg-white z-20 relative">
                
                <a href="/" class="flex items-center gap-3 group select-none">
                    <div class="relative w-10 h-10 border-2 border-black bg-[#F9BA72] 
                                flex items-center justify-center shadow-[3px_3px_0_0_#000] 
                                group-hover:bg-[#41B78E] group-hover:translate-x-0.5 group-hover:translate-y-0.5 
                                group-hover:shadow-none transition-all duration-200">
                        <div class="grid grid-cols-2 gap-0.5">
                            <div class="w-1.5 h-1.5 bg-black"></div>
                            <div class="w-1.5 h-1.5 bg-white"></div>
                            <div class="w-1.5 h-1.5 bg-white"></div>
                            <div class="w-1.5 h-1.5 bg-black"></div>
                        </div>
                    </div>
                    <div class="flex flex-col -gap-1">
                        <span class="font-bold text-2xl leading-none tracking-tight text-black">PIXEL.</span>
                        <span class="text-xs font-bold tracking-[0.2em] text-[#F9BA72] group-hover:text-[#41B78E] transition-colors">STUDIO</span>
                    </div>
                </a>

                <div class="hidden md:flex items-center gap-8">
                    {#each navLinks as link}
                        <a href={link.href} 
                           class="relative font-semibold text-base uppercase tracking-wider text-slate-700 
                                  hover:text-[#F9BA72] transition-colors py-1 group">
                            {link.name}
                            <span class="absolute bottom-0 left-0 w-full h-0.75 bg-[#41B78E] scale-x-0 
                                       group-hover:scale-x-100 transition-transform origin-left duration-300"></span>
                        </a>
                    {/each}
                </div>

                <div class="flex items-center gap-4">
                    <button class="hidden md:block bg-[#F9BA72] text-white border-2 border-black px-6 py-2 
                                   font-bold uppercase tracking-wider text-sm shadow-[4px_4px_0_0_#000] 
                                   hover:bg-[#41B78E] hover:text-white
                                   hover:translate-x-0.5 hover:translate-y-0.5 hover:shadow-[2px_2px_0_0_#000] 
                                   active:shadow-none active:translate-x-1 active:translate-y-1 transition-all duration-200">
                        Let's Talk
                    </button>

                    <button onclick={toggleMenu} aria-label="Toggle Menu"
                            class="md:hidden w-11 h-11 border-2 border-black bg-[#41B78E] flex flex-col justify-center items-center gap-1.5 
                                   shadow-[3px_3px_0_0_#000] hover:bg-[#F9BA72]
                                   active:translate-x-0.5 active:translate-y-0.5 active:shadow-none transition-all duration-200">
                        <span class="w-6 h-0.75 bg-black transition-transform duration-300 {isMenuOpen ? 'rotate-45 translate-y-2.25' : ''}"></span>
                        <span class="w-6 h-0.75 bg-black transition-opacity duration-300 {isMenuOpen ? 'opacity-0' : 'opacity-100'}"></span>
                        <span class="w-6 h-0.75 bg-black transition-transform duration-300 {isMenuOpen ? '-rotate-45 -translate-y-2.25' : ''}"></span>
                    </button>
                </div>
            </div>

            {#if isMenuOpen}
                <div transition:slide={{ duration: 300, easing: cubicOut, axis: 'y' }} 
                     class="border-t-[3px] border-black bg-slate-50 md:hidden flex flex-col p-4 gap-2 shadow-inner">
                    
                    {#each navLinks as link}
                        <a href={link.href} onclick={() => isMenuOpen = false}
                           class="block w-full border-2 border-transparent 
                                  hover:border-black hover:bg-[#41B78E] hover:text-white
                                  px-4 py-3 font-semibold uppercase text-base text-slate-700 
                                  transition-all duration-200 hover:shadow-[3px_3px_0_0_#000]">
                            {link.name}
                        </a>
                    {/each}
                    
                    <div class="h-px bg-slate-300 my-2"></div>

                    <button class="w-full bg-[#F9BA72] text-white border-2 border-black py-3 
                                   font-bold uppercase tracking-wider text-sm shadow-[3px_3px_0_0_#000] 
                                   hover:bg-[#41B78E] hover:text-white
                                   active:shadow-none active:translate-x-0.5 active:translate-y-0.5 transition-colors duration-200">
                        Contact Us
                    </button>
                </div>
            {/if}

        </div>
    </div>
</nav>

<!-- svelte-ignore slot_element_deprecated -->
<div class="pt-32">
    <slot />
</div>

<style>
    nav {
        font-family: 'Pixelify Sans', sans-serif;
        letter-spacing: 0.02em; 
    }
</style>