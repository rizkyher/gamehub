<script lang="ts">
  import { fade, fly } from "svelte/transition";
  import { cubicIn } from "svelte/easing";

  // Import Komponen UI
  import Navbar from "$lib/components/ui/navbar/Navbar.svelte";
  import Clouds from "$lib/components/ui/Clouds.svelte";
  import Header from "$lib/components/ui/Header.svelte";
  import GameTrailer from "$lib/components/ui/GameTrailer.svelte";
  import GameCard from "$lib/components/ui/GameCard.svelte";
  import About from "$lib/components/ui/About.svelte";
  import Team from "$lib/components/ui/Team.svelte";
  import Footer from "$lib/components/ui/Footer.svelte";
  import LoadingsScreen from "$lib/components/ui/LoadingsScreen.svelte";

  // State untuk loading screen
  let isLoading = $state(true);

  function handleLoadingComplete() {
    isLoading = false;
  }

  // Data Game
  let myGames = $state([
    {
      id: 1,
      title: "Writing Hijaiyah",
      desc: "Belajar menulis huruf hijaiyah dengan cara yang menyenangkan dan interaktif untuk anak-anak.",
      tags: ["Educational", "Kids"],
      image: "/writing.jpg",
      playUrl: "https://gd.games/instant-builds/41e5f344-d10c-496c-9538-70928971dff8",
    },
    {
      id: 2,
      title: "Santri Running",
      desc: "Petualangan platformer bertema budaya santri. Kumpulkan ayat Al-Qur'an sambil menghindari rintangan.",
      tags: ["Runner", "Action"],
      image: "/Santri.jpg",
      playUrl: "https://gd.games/ghp-game/santri-running",
    },
    {
      id: 3,
      title: "Flappy Hijaiyah",
      desc: "Terbang melewati rintangan sambil mengumpulkan huruf hijaiyah yang benar. Melatih fokus dan ingatan.",
      tags: ["Arcade", "Casual"],
      image: "/flappy.jpg",
      playUrl: "https://gd.games/instant-builds/9ab745ac-3112-4c67-bd19-ad9b12d3c14c",
    },
    {
      id: 4,
      title: "Salman Al-farisi",
      desc: "Ikuti kisah heroik sahabat Nabi, Salman Al-Farisi, dalam game petualangan strategi yang mendalam.",
      tags: ["Adventure", "History"],
      image: "/salman.jpg",
      playUrl: "https://farrelnashwan33.itch.io/the-seeker-of-light",
    },
    {
      id: 5,
      title: "Match 3 Hijaiyah",
      desc: "Game puzzle klasik. Cocokkan 3 huruf hijaiyah yang sama untuk mendapatkan skor tertinggi.",
      tags: ["Puzzle", "Logic"],
      image: "/match3.jpeg",
      playUrl: "https://gd.games/instant-builds/8f743407-34c7-449a-9acc-1bc6ee73463e",
    },
    {
      id: 6,
      title: "Catching The Hijaiyah",
      desc: "Latih ketangkasanmu dengan menangkap huruf hijaiyah yang jatuh dari langit sesuai instruksi.",
      tags: ["Educational", "Speed"],
      image: "/Catching.jpeg",
      playUrl: "https://gd.games/instant-builds/159d1ac7-af12-4d0d-b24b-a5263b4d028c",
    },
  ]);

  // Data Tim (SUDAH DIPERBAIKI: menggunakan photoUrl)
  let myTeam = $state([
    {
      name: "Bayu",
      role: "Developer Game",
      avatarColor: "bg-[#41B78E]",
      bio: "WRITING HIJAIYAH.",
      photoUrl: "/bayu.jpg",
    },
    {
      name: "Zaidan",
      role: "Developer Game",
      avatarColor: "bg-[#F9BA72]",
      bio: "SANTRI BROS.",
      photoUrl: "/zaidan.jpg",
    },
    {
      name: "Zain",
      role: "Developer Game",
      avatarColor: "bg-slate-300",
      bio: "WRITING HIJAIYAH.",
      photoUrl: "/zain.jpg",
    },
    {
      name: "Arif",
      role: "Developer Game",
      avatarColor: "bg-slate-300",
      bio: "VISULA NOVE SALMAN AL-FARISI.",
      photoUrl: "/arif.jpg",
    },
    {
      name: "Farhan",
      role: "Developer Game",
      avatarColor: "bg-slate-300",
      bio: "SANTRI BROS.",
      photoUrl: "/farhan.jpg",
    },
    {
      name: "Farrel",
      role: "Developer Game",
      avatarColor: "bg-slate-300",
      bio: "VISULA NOVE SALMAN AL-FARISI.",
      photoUrl: "/farrel.jpg",
    },
    {
      name: "Aab",
      role: "Developer Game",
      avatarColor: "bg-slate-300",
      bio: "DUPALO.",
      photoUrl: "/aab.jpg",
    },
  ]);
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />

  <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&family=VT323&display=swap" rel="stylesheet" />

  <title>Khwarizmi Game Hub</title>
  <link rel="icon" href="/logo.jpg" />
</svelte:head>

{#if isLoading}
  <div out:fly={{ y: -1000, duration: 1200, easing: cubicIn }} class="fixed inset-0 z-9999">
    <LoadingsScreen onComplete={handleLoadingComplete} />
  </div>
{:else}
  <div in:fade={{ duration: 1000, delay: 400 }}>
    <Clouds />

    <Navbar />

    <main class="relative z-10 min-h-screen font-pixel overflow-x-hidden">
      <div class="max-w-6xl mx-auto px-6 py-12">
        <section id="home">
          <Header title="K H W A R I Z M I" subtitle="Khawrizmi Game Hub adalah kumpulan game interaktif Islami untuk membantu anak belajar huruf Hijaiyah, Al-Qur'an, dan mengenal Sahabat Rasulullah SAW dengan lebih menyenangkan." />
        </section>

        <section class="mt-12 mb-24 flex justify-center">
          <GameTrailer videoSrc="Videogame.mp4" title="Project: Horizon 2026" />
        </section>

        <div class="my-20 flex justify-center items-center gap-4 opacity-60">
          <div class="h-0.75 grow bg-black rounded-full"></div>
          <div class="w-6 h-6 bg-[#F9BA72] border-[3px] border-black rotate-45 shadow-[3px_3px_0_0_#41B78E]"></div>
          <div class="h-0.75 grow bg-black rounded-full"></div>
        </div>

        <section id="games" class="scroll-mt-32 overflow-hidden">
          <div class="flex justify-between items-end mb-12 px-2">
            <h2 class="text-4xl md:text-5xl font-bold text-slate-900 uppercase italic leading-none">
              Featured <span class="text-[#41B78E] underline decoration-[#F9BA72] decoration-4 underline-offset-4">Games</span>
            </h2>

            <div class="hidden md:block text-xs font-bold bg-black text-[#F9BA72] px-4 py-2 border-2 border-transparent shadow-[4px_4px_0_0_#41B78E] uppercase tracking-wider animate-pulse">Shift + Scroll →</div>
          </div>

          <div class="flex overflow-x-auto gap-8 pb-16 pt-4 px-2 no-scrollbar snap-x snap-mandatory scroll-smooth">
            {#each myGames as game (game.id)}
              <GameCard {game} />
            {/each}
          </div>
        </section>

        <section id="about" class="scroll-mt-32 mb-20">
          <About />
        </section>

        <section id="team" class="scroll-mt-32">
          <Team members={myTeam} />
        </section>
      </div>

      <Footer creator="Khwarizmi" />
    </main>
  </div>
{/if}

<style>
  .font-pixel {
    font-family: "Pixelify Sans", sans-serif;
  }

  :global(html) {
    scroll-behavior: smooth;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: "Pixelify Sans", sans-serif;
    background-color: #f8fafc;
    color: #0f172a;
    overflow-x: hidden;
  }

  .no-scrollbar::-webkit-scrollbar {
    display: none;
  }
  .no-scrollbar {
    -ms-overflow-style: none;
    scrollbar-width: none;
  }

  :global(::-webkit-scrollbar) {
    width: 14px;
  }
  :global(::-webkit-scrollbar-track) {
    background: #0f172a;
    border-left: 2px solid #000;
  }
  :global(::-webkit-scrollbar-thumb) {
    background: #f9ba72;
    border: 3px solid #000;
    border-radius: 0;
  }
  :global(::-webkit-scrollbar-thumb:hover) {
    background: #41b78e;
  }
</style>
