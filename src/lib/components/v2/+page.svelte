<script lang="ts">
  import Navbar from "$lib/components/ui/navbar/Navbar.svelte";
  import Hero from "$lib/components/ui/hero/Hero.svelte";
  import GameList from "$lib/components/ui/game/GameList.svelte";
  import GameFilter from "$lib/components/ui/game/GameFilter.svelte";
  import DevShowcase from "$lib/components/ui/game/DeveloperShowcase.svelte";
  import About from "$lib/components/ui/game/About.svelte";
  import Footer from "$lib/components/ui/footer/Footer.svelte";
  import { ArrowUp } from "@lucide/svelte";
  import { fade, fly } from "svelte/transition";

  // Svelte 5 State
  let activeCategory = $state("All Games");
  let scrollY = $state(0);
  let innerHeight = $state(0);

  // Logic untuk tombol Back to Top
  let showBackToTop = $derived(scrollY > 500);

  function handleScroll() {
    scrollY = window.scrollY;
  }

  function scrollToTop() {
    window.scrollTo({ top: 0, behavior: "smooth" });
  }
</script>

<svelte:window onscroll={handleScroll} bind:innerHeight />

<svelte:head>
  <title>GHP Studio | Spirit of Pixel</title>
  <style>
    @import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");

    :root {
      --ghibli-grass: #606c38;
      --ghibli-cream: #fefae0;
      --ghibli-wood: #bc6c25;
      --ghibli-dark-wood: #283618;
      --ghibli-sand: #f1f0e8;
      --ghibli-sky: #a8dadc;
      --ghibli-accent: #e76f51;
    }

    body {
      background-color: var(--ghibli-sand);
      font-family: "VT323", monospace;
      margin: 0;
      overflow-x: hidden;
      /* Custom Cursor agar imersi terjaga */
      cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" style="fill:black;stroke:white;stroke-width:2px;"><path d="M5.5 3.21l10.85 10.87-4.57 1.05 4.09 7.15-2.6 1.49-4.11-7.14-3.32 3.09V3.21z"/></svg>'),
        auto;
    }

    ::selection {
      background: var(--ghibli-wood);
      color: var(--ghibli-cream);
    }
  </style>
</svelte:head>

<div class="page-container">
  <div class="atmosphere-layer">
    <div class="sky-gradient"></div>

    {#each Array(6) as _, i}
      <div
        class="cloud-wrapper"
        style="
          top: {5 + i * 15}%; 
          animation-duration: {40 + i * 10}s;
          opacity: {0.4 + i * 0.1};
          transform: scale({0.5 + i * 0.15});
        "
      >
        <div class="cloud-body"></div>
      </div>
    {/each}

    {#each Array(20) as _, i}
      <div
        class="particle"
        style="
          left: {Math.random() * 100}%;
          animation-delay: {Math.random() * 10}s;
          animation-duration: {15 + Math.random() * 20}s;
        "
      >
        {["🍃", "🌾", "✨"][Math.floor(Math.random() * 3)]}
      </div>
    {/each}
  </div>

  <div class="texture-overlay noise"></div>
  <div class="texture-overlay vignette"></div>
  <div class="texture-overlay warm-filter"></div>

  <Navbar bind:activeCategory />

  <main class="relative z-10">
    <section id="home" class="relative">
      <Hero />
      <div class="paper-tear-divider"></div>
    </section>

    <section id="archive" class="archive-section relative">
      <div class="hidden xl:block absolute top-20 left-10 opacity-40 pointer-events-none">
        <div class="flex flex-col gap-8 text-4xl text-[#606c38] animate-float-slow">
          <span>🍄</span><span>🌿</span><span>🪵</span>
        </div>
      </div>

      <div class="container mx-auto px-4 md:px-6 relative z-10 pt-20 pb-32">
        <div class="flex flex-col items-center mb-16 relative">
          <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[300px] h-[300px] bg-[#bc6c25]/5 rounded-full blur-3xl -z-10"></div>

          <div class="border-y-2 border-[#283618] py-2 px-8 mb-4 bg-[#fefae0]/80 backdrop-blur-sm rotate-1 shadow-sm">
            <span class="font-['VT323'] text-[#606c38] text-xl tracking-[0.3em] uppercase">The Collection</span>
          </div>

          <h2 class="text-6xl md:text-8xl text-[#283618] mb-2 drop-shadow-sm relative">
            <span class="relative z-10">GAME_ARCHIVE</span>
            <span class="absolute -bottom-4 -right-8 text-3xl md:text-4xl text-[#bc6c25] -rotate-6 font-bold font-sans opacity-80" style="font-family: cursive;">Index 01</span>
          </h2>

          <div class="mt-8 relative group">
            <div class="absolute inset-0 bg-[#283618] translate-x-1 translate-y-1 rounded-lg"></div>
            <div class="relative bg-[#fefae0] border-2 border-[#283618] rounded-lg p-2 z-10">
              <GameFilter bind:selected={activeCategory} />
            </div>
          </div>
        </div>

        <div id="showcase" class="min-h-[500px]">
          <GameList filter={activeCategory} />
        </div>
      </div>

      <div class="absolute bottom-0 left-0 w-full leading-none overflow-hidden rotate-180">
        <svg data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 120" preserveAspectRatio="none" class="relative block w-[calc(100%+1.3px)] h-[80px] md:h-[150px]">
          <path d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V0H0V27.35A600.21,600.21,0,0,0,321.39,56.44Z" class="fill-[#f1f0e8]"
          ></path>
        </svg>
      </div>
    </section>

    <section class="bg-[#f1f0e8] pt-20 pb-32 relative overflow-hidden">
      {#each Array(5) as _, i}
        <div class="absolute opacity-30 animate-float-diagonal pointer-events-none text-[#bc6c25]" style="top: {Math.random() * 100}%; left: -5%; animation-delay: {i * 3}s; animation-duration: {15 + i * 2}s; font-size: 2rem;">ꕥ</div>
      {/each}

      <DevShowcase />
    </section>

    <section id="about" class="relative z-20">
      <About />
    </section>
  </main>

  <Footer />

  {#if showBackToTop}
    <button transition:fly={{ y: 50, duration: 500 }} onclick={scrollToTop} class="fixed bottom-8 right-8 z-50 group" aria-label="Back to top">
      <div class="relative w-14 h-14 bg-[#283618] rounded-full flex items-center justify-center shadow-lg border-2 border-[#fefae0] group-hover:scale-110 transition-transform duration-300">
        <div class="absolute top-4 left-3 w-3 h-3 bg-white rounded-full"><div class="absolute top-1 right-1 w-1 h-1 bg-black rounded-full"></div></div>
        <div class="absolute top-4 right-3 w-3 h-3 bg-white rounded-full"><div class="absolute top-1 left-1 w-1 h-1 bg-black rounded-full"></div></div>

        <ArrowUp class="text-[#fefae0] mt-3 group-hover:-translate-y-1 transition-transform" size={20} strokeWidth={3} />
      </div>
      <span class="absolute -bottom-6 left-1/2 -translate-x-1/2 text-xs font-bold text-[#283618] opacity-0 group-hover:opacity-100 transition-opacity">UP!</span>
    </button>
  {/if}
</div>

<style>
  /* ===== ANIMATIONS ===== */
  @keyframes float-slow {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-20px);
    }
  }
  .animate-float-slow {
    animation: float-slow 6s ease-in-out infinite;
  }

  @keyframes float-diagonal {
    0% {
      transform: translate(0, 0) rotate(0deg);
      opacity: 0;
    }
    20% {
      opacity: 0.6;
    }
    80% {
      opacity: 0.6;
    }
    100% {
      transform: translate(100vw, -50vh) rotate(360deg);
      opacity: 0;
    }
  }
  .animate-float-diagonal {
    animation-name: float-diagonal;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  /* ===== ATMOSPHERE ===== */
  .atmosphere-layer {
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
    overflow: hidden;
  }

  .sky-gradient {
    position: absolute;
    inset: 0;
    background: linear-gradient(180deg, #e0fbfc 0%, #fefae0 60%, #faedcd 100%);
  }

  /* Cloud CSS Only Approach (Lebih performant dari SVG inline banyak) */
  .cloud-wrapper {
    position: absolute;
    left: -20%;
    animation-name: moveClouds;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  .cloud-body {
    width: 200px;
    height: 60px;
    background: #fff;
    border-radius: 200px;
    position: relative;
    box-shadow: 0 4px 0 rgba(0, 0, 0, 0.05);
  }
  .cloud-body::after,
  .cloud-body::before {
    content: "";
    position: absolute;
    background: #fff;
    border-radius: 50%;
  }
  .cloud-body::after {
    width: 80px;
    height: 80px;
    top: -40px;
    left: 30px;
  }
  .cloud-body::before {
    width: 60px;
    height: 60px;
    top: -30px;
    left: 90px;
  }

  @keyframes moveClouds {
    0% {
      transform: translateX(0);
    }
    100% {
      transform: translateX(120vw);
    }
  }

  .particle {
    position: absolute;
    top: -10%;
    opacity: 0;
    font-size: 1.2rem;
    animation-name: fallParticles;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  @keyframes fallParticles {
    0% {
      transform: translateY(0) rotate(0deg);
      opacity: 0;
    }
    10% {
      opacity: 0.8;
    }
    90% {
      opacity: 0.8;
    }
    100% {
      transform: translateY(110vh) rotate(360deg);
      opacity: 0;
    }
  }

  /* ===== TEXTURES ===== */
  .texture-overlay {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 50; /* Di atas konten tapi di bawah modal */
  }

  .noise {
    background-image: url("https://www.transparenttextures.com/patterns/p6.png"); /* Noise halus */
    opacity: 0.08;
    mix-blend-mode: multiply;
  }

  .vignette {
    background: radial-gradient(circle, transparent 50%, rgba(40, 54, 24, 0.15) 100%);
  }

  .warm-filter {
    background-color: #fca311;
    opacity: 0.03;
    mix-blend-mode: overlay; /* Efek Golden Hour */
  }

  /* ===== SECTION STYLES ===== */
  .archive-section {
    background-color: #fefae0;
    background-image: radial-gradient(#606c38 0.5px, transparent 0.5px);
    background-size: 20px 20px; /* Dot Grid halus */
  }

  /* Paper Tear Effect (CSS Masking approach alternative or SVG border) */
  .paper-tear-divider {
    position: absolute;
    bottom: -1px;
    left: 0;
    width: 100%;
    height: 40px;
    background-color: #fefae0; /* Warna section berikutnya */
    mask-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 100 20' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M0 20 L0 0 L10 10 L20 0 L30 10 L40 0 L50 10 L60 0 L70 10 L80 0 L90 10 L100 0 L100 20 Z' fill='black'/%3E%3C/svg%3E");
    mask-repeat: repeat-x;
    mask-size: 40px 100%;
    z-index: 5;
  }
</style>
