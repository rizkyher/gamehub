<script lang="ts">
  import { fade, fly } from "svelte/transition";
  // 1. Tambahkan 'Users' ke import icon
  import { Menu, X, Gamepad2, Home, User, Users } from "@lucide/svelte";

  // Props
  let { activeCategory = $bindable() } = $props();

  // State
  let menuOpen = $state(false);
  let scrollY = $state(0);

  // Derived State
  let isScrolled = $derived(scrollY > 20);

  // DATA NAVIGASI
  // 2. Tambahkan 'Team' di sini
  const navLinks = [
    { name: "Home", icon: Home, target: "home" },
    { name: "Games", icon: Gamepad2, target: "games" },
    { name: "About", icon: User, target: "about" },
    { name: "Team", icon: Users, target: "team" }, // <-- Menu Team Ditambahkanx`
  ];

  function selectMenu(name: string, target?: string) {
    activeCategory = name;
    menuOpen = false;

    if (!target) return;

    const el = document.getElementById(target);
    if (!el) return;

    el.scrollIntoView({
      behavior: "smooth",
      block: "start",
    });
  }
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<svelte:window bind:scrollY={scrollY} />

<nav class="fixed top-0 left-0 right-0 z-100 transition-all duration-300 ease-out {isScrolled ? 'py-2' : 'py-4 md:py-8'} font-pixel">
  <div class="max-w-7xl mx-auto px-4 md:px-8">
    <div class="flex items-center justify-between">
      
      <button
        onclick={() => selectMenu("Home", "home")}
        class="group relative flex items-center bg-white border-[3px] border-black p-1 shadow-[4px_4px_0px_0px_#000] hover:shadow-none hover:translate-x-0.5 hover:translate-y-0.5 transition-all"
      >
        <img 
            src="/logo.jpg" 
            alt="Khwarizmi Logo" 
            class="w-7 h-7 object-contain block ml-1"
        />

        <div class="px-3 py-1 bg-white">
          <h1 class="text-2xl text-black leading-none uppercase tracking-tighter font-bold">Khwarizmi</h1>
          <p class="text-[10px] text-[#F9BA72] leading-none uppercase tracking-[0.2em] font-bold group-hover:text-[#41B78E] transition-colors">GAME HUB</p>
        </div>
      </button>

      <div class="hidden md:flex items-center gap-4">
        {#each navLinks as link}
          <button
            onclick={() => selectMenu(link.name, link.target)}
            class="group relative px-6 py-2 flex items-center gap-2 border-[3px] border-black transition-all duration-200
            {activeCategory === link.name 
                ? 'bg-[#F9BA72] text-white -translate-y-1 shadow-[4px_4px_0px_0px_#000]' 
                : 'bg-white text-slate-700 hover:-translate-y-1 hover:shadow-[4px_4px_0px_0px_#41B78E] hover:text-[#F9BA72]'}"
          >
            <span class="text-sm group-hover:scale-110 transition-transform">
                <link.icon size={20} />
            </span>
            <span class="text-lg uppercase tracking-widest font-bold">{link.name}</span>

            {#if activeCategory === link.name}
              <div in:fade class="absolute -bottom-4 left-1/2 -translate-x-1/2 text-[#F9BA72] text-xs">▲</div>
            {/if}
          </button>
        {/each}
      </div>

      <button
        class="md:hidden size-12 bg-[#41B78E] border-[3px] border-black shadow-[4px_4px_0px_0px_#000] flex items-center justify-center text-white active:shadow-none active:translate-y-1 transition-all hover:bg-[#F9BA72] hover:text-black"
        onclick={() => (menuOpen = !menuOpen)}
      >
        {#if menuOpen}
          <X size={28} />
        {:else}
          <Menu size={28} />
        {/if}
      </button>
    </div>
  </div>

  {#if menuOpen}
    <div transition:fade={{ duration: 200 }} class="fixed inset-0 bg-white/95 z-[-1] flex flex-col items-center justify-center p-6 overflow-hidden mt-20">
      <div class="absolute inset-0 opacity-10" 
           style="background-image: repeating-linear-gradient(45deg, #F9BA72 0, #F9BA72 2px, transparent 0, transparent 50%); background-size: 10px 10px;">
      </div>

      <div class="absolute top-20 left-10 text-6xl animate-pulse opacity-50">👾</div>
      <div class="absolute bottom-40 right-10 text-6xl animate-bounce opacity-50">🎮</div>

      <div class="flex flex-col gap-4 w-full max-w-xs relative z-10">
        {#each navLinks as link, i}
          <button
            in:fly={{ y: 20, delay: i * 100 }}
            onclick={() => selectMenu(link.name, link.target)}
            class="w-full bg-white border-[3px] border-black p-4 flex items-center justify-between 
                   shadow-[6px_6px_0px_0px_#41B78E] 
                   hover:bg-[#F9BA72] hover:text-black hover:shadow-[6px_6px_0px_0px_#000]
                   active:shadow-none active:translate-x-1 active:translate-y-1 transition-all group"
          >
            <span class="text-3xl uppercase tracking-tight font-bold group-hover:tracking-widest transition-all">{link.name}</span>
            <span class="text-3xl"><link.icon size={28}/></span>
          </button>
        {/each}
      </div>
    </div>
  {/if}
</nav>

<style>
  .font-pixel {
    font-family: 'Pixelify Sans', sans-serif;
  }
</style>