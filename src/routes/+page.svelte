<script lang="ts">
    // 1. Import Komponen
    import Navbar from '$lib/components/ui/navbar/Navbar.svelte';
    import Clouds from '$lib/components/ui/Clouds.svelte';
    import Header from '$lib/components/ui/Header.svelte';
    import GameTrailer from '$lib/components/ui/GameTrailer.svelte';
    import GameCard from '$lib/components/ui/GameCard.svelte';
    import About from '$lib/components/ui/About.svelte';
    import Team from '$lib/components/ui/Team.svelte';
    import Footer from '$lib/components/ui/Footer.svelte';

    // 2. Data Game
    let myGames = $state([
        { 
            id: 1, 
            title: "Writing Hijaiyah", 
            desc: "Permainan edukasi interaktif untuk membantu anak-anak belajar menulis huruf hijaiyah dengan cara yang menyenangkan.", 
            tags: ["Educational", "Kids"], 
            image: "/writing.jpg",
            playUrl: "https://gd.games/instant-builds/05d45ddc-a588-4047-93dd-4f4cc0166a83" 
        },
        { 
            id: 2, 
            title: "Santri Running", // Typo Fixed: Runing -> Running
            desc: "Petualangan platformer bertema budaya. Hadapi rintangan sambil mengumpulkan ayat-ayat Al-Qur'an.", 
            tags: ["Runner", "Action"], 
            image: "/santri.jpg",
            playUrl: "https://gd.games/ghp-game/santri-running" 
        }, 
        { 
            id: 3, 
            title: "Flappy Hijaiyah", 
            desc: "Gameplay klasik Flappy Bird dengan sentuhan edukasi. Hindari rintangan dan kumpulkan huruf yang tepat.", 
            tags: ["Arcade", "Casual"], 
            image: "/Flappy.jpg", 
            playUrl: "#" // Link belum tersedia
        },
        { 
            id: 4, 
            title: "Salman Alfarisi", 
            desc: "Kisah heroik sahabat nabi dalam bentuk game petualangan strategi yang mendalam.", 
            tags: ["Adventure", "History"], 
            image: "/salman.jpg",
            playUrl: "https://farrelnashwan33.itch.io/the-seeker-of-light"
        }, 
        { 
            id: 5, 
            title: "Match 3 Hijaiyah", 
            desc: "Cocokkan huruf hijaiyah yang sama untuk mendapatkan skor tertinggi.", 
            tags: ["Puzzle", "Logic"], 
            image: "/match3.jpeg",
            playUrl: "https://gd.games/instant-builds/8f743407-34c7-449a-9acc-1bc6ee73463e" 
        },
        { 
            id: 6, 
            title: "Catching The Hijaiyah", 
            desc: "Latih ketangkasanmu dengan menangkap huruf yang jatuh dari langit sesuai instruksi.", 
            tags: ["Educational", "Speed"], 
            image: "/Catching.jpeg",
            playUrl: "https://gd.games/instant-builds/159d1ac7-af12-4d0d-b24b-a5263b4d028c" 
        }
    ]);

    // 3. Data Team
    let myTeam = $state([
        { 
            name: "Bayu", 
            role: "Lead Developer", 
            avatarColor: "bg-[#41B78E]", 
            bio: "Spesialis Svelte & Sihir Kode.", 
            photoUrl: "/bayu.jpeg" 
        },
        { 
            name: "Zaidan", 
            role: "Pixel Artist", 
            avatarColor: "bg-[#F9BA72]", 
            bio: "Melukis dunia dengan kotak.", 
            photoUrl: "/zaidan.jpeg" 
        },
        { 
            name: "Zain", 
            role: "Game Designer", 
            avatarColor: "bg-slate-300", 
            bio: "Penjaga atmosfer game.", 
            photoUrl: "/zain.jpeg" 
        },
        { 
            name: "Arif", 
            role: "Game Designer", 
            avatarColor: "bg-slate-300", 
            bio: "Penjaga atmosfer game.", 
            photoUrl: "/arif.jpeg" 
        },
        { 
            name: "Farhan", 
            role: "Game Designer", 
            avatarColor: "bg-slate-300", 
            bio: "Penjaga atmosfer game.", 
            photoUrl: "/farhan.jpeg" 
        },
        { 
            name: "Farrel", 
            role: "Game Designer", 
            avatarColor: "bg-slate-300", 
            bio: "Penjaga atmosfer game.", 
            photoUrl: "/farrel.jpeg" 
        },
    ]);
</script>

<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
</svelte:head>

<Clouds />

<Navbar />

<main class="relative z-10 min-h-screen font-pixel overflow-x-hidden">
    <div class="max-w-6xl mx-auto px-6 py-12">
        
        <section id="home">
            <Header 
                title="K H W A R I Z M I" 
                subtitle="Koleksi petualangan kecil dalam balutan pixel art dan estetika Ghibli." 
            />
        </section>

        <section class="mt-12 mb-24 flex justify-center">
            <GameTrailer 
                videoSrc="vario.mp4" 
                title="Project: Horizon 2026" 
            />
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
                
                <div class="hidden md:block text-xs font-bold bg-black text-[#F9BA72] px-4 py-2 border-2 border-transparent shadow-[4px_4px_0_0_#41B78E] uppercase tracking-wider animate-pulse">
                    Shift + Scroll →
                </div>
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

<style>
    /* Menggunakan Font Global */
    .font-pixel {
        font-family: 'Pixelify Sans', sans-serif;
    }

    :global(html) { scroll-behavior: smooth; }
    
    :global(body) {
        margin: 0; padding: 0;
        font-family: 'Pixelify Sans', sans-serif;
        background-color: #f8fafc; 
        color: #0f172a;
        overflow-x: hidden;
    }

    /* Hide Scrollbar for Horizontal Gallery */
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

    /* Custom Browser Scrollbar (Theme Styled) */
    :global(::-webkit-scrollbar) { width: 14px; }
    :global(::-webkit-scrollbar-track) { background: #0f172a; border-left: 2px solid #000; }
    :global(::-webkit-scrollbar-thumb) { 
        background: #F9BA72; 
        border: 3px solid #000; 
        border-radius: 0;
    }
    :global(::-webkit-scrollbar-thumb:hover) { background: #41B78E; }
</style>