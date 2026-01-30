<script lang="ts">
  import { Instagram, Youtube, MessageCircle, Heart } from "lucide-svelte";
  import { onMount } from "svelte";

  let mounted = $state(false);
  const currentYear = new Date().getFullYear();

  onMount(() => {
    setTimeout(() => {
      mounted = true;
    }, 100);
  });

  const footerLinks = {
    product: ["Features", "Pricing", "Integrations", "Changelog"],
    company: ["About Us", "Careers", "Blog", "Contact"],
    legal: ["Privacy Policy", "Terms of Service", "Cookie Policy"],
  };

  const socialLinks = [
    {
      icon: Instagram,
      href: "https://www.instagram.com/sekolahimpianofficial/",
      label: "Instagram",
      colorClass: "hover:text-pink-500 hover:border-pink-500 hover:bg-pink-500/10 hover:shadow-pink-500/20",
    },
    {
      icon: Youtube,
      href: "https://www.youtube.com/@sekolahimpianku",
      label: "YouTube",
      colorClass: "hover:text-red-500 hover:border-red-500 hover:bg-red-500/10 hover:shadow-red-500/20",
    },
    {
      icon: MessageCircle, // Lucide substitute untuk WhatsApp
      href: "https://api.whatsapp.com/send/?phone=6281282251136&text&type=phone_number&app_absent=0",
      label: "WhatsApp",
      colorClass: "hover:text-green-500 hover:border-green-500 hover:bg-green-500/10 hover:shadow-green-500/20",
    },
  ];
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap" rel="stylesheet" />
</svelte:head>

<footer class="relative mt-40 w-full font-pixel overflow-hidden text-[#FFE4C4] select-none">
  <div class="absolute inset-0 h-64 bg-linear-to-b from-[#87CEEB] via-[#F9BA72] to-[#FFD700] z-0 pointer-events-none overflow-hidden">
    <div class="absolute top-10 right-20 w-16 h-16 bg-[#F9BA72] border-4 border-[#FFD700] shadow-[4px_4px_0_0_#FF4500] animate-pulse-slow"></div>
    <div class="absolute top-20 left-0 w-32 h-12 bg-white opacity-80 animate-cloud-drift-slow delay-0"></div>
    <div class="absolute top-5 right-1/3 w-24 h-8 bg-white opacity-60 animate-cloud-drift-fast delay-1000"></div>
  </div>

  <div class="absolute top-32 inset-x-0 h-32 z-10 pointer-events-none">
    {#each Array(6) as _, i}
      <div
        class="absolute bottom-0 w-0 h-0
                    border-l-60 border-r-60 border-b-100
                    border-l-transparent border-r-transparent border-b-[#4A6741]"
        style="left: {i * 15}%; transform: scale({1 + (i % 2) * 0.3}); z-index: {i};"
      >
        <div
          class="absolute -left-5 -top-7.5 w-0 h-0
                         border-l-20 border-r-20 border-b-30
                         border-l-transparent border-r-transparent border-b-white"
        ></div>
      </div>
    {/each}
  </div>

  <div
    class="relative z-20 bg-[#5D4037] border-t-8 border-[#2E7D32] pt-16 pb-8
              before:content-[''] before:absolute before:-top-2 before:left-0 before:w-full before:h-2 before:bg-[url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAFklEQVQYV2NkYGD4z4AHYGNgYCQHAQCIYwH5S8XJ8wAAAABJRU5ErkJggg==')] before:opacity-50"
  >
    <div class="absolute -top-10 left-0 animate-walk-across pointer-events-none">
      <div class="w-8 h-12 bg-red-500 border-2 border-black relative">
        <div class="absolute top-1 left-1 w-2 h-2 bg-white"></div>
        <div class="absolute bottom-0 left-1 w-2 h-3 bg-blue-700 animate-leg-walk"></div>
        <div class="absolute bottom-0 right-1 w-2 h-3 bg-blue-700 animate-leg-walk delay-150"></div>
      </div>
    </div>

    <div class="max-w-7xl mx-auto px-6 relative z-30" class:opacity-0={!mounted} class:animate-fade-in-up={mounted}>
      <div class="grid grid-cols-1 md:grid-cols-4 gap-10 mb-12">
        <div class="col-span-1 md:col-span-2 space-y-6">
          <button
            class="group relative inline-block bg-[#8D6E63] border-4 border-[#3E2723] p-4
                           shadow-[8px_8px_0_0_#2E7D32]
                           hover:shadow-none hover:translate-x-1.5 hover:translate-y-1.5
                           active:scale-95
                           transition-all duration-150 cursor-pointer outline-none overflow-hidden"
          >
            <h2 class="text-3xl font-bold uppercase tracking-widest leading-none text-white flex items-center gap-4 relative z-10">
              <span class="text-4xl filter drop-shadow-md group-hover:animate-spin-pixel">🍄</span>

              <span class="relative inline-block group-hover:animate-glitch" data-text="Khwarizmi"> Khawrizmi </span>
            </h2>

            <div class="absolute top-0 -left-full w-1/2 h-full bg-linear-to-r from-transparent via-white/30 to-transparent skew-x-[-25deg] group-hover:animate-shine pointer-events-none"></div>
          </button>

          <p class="font-bold text-lg leading-relaxed max-w-sm border-l-4 border-[#F9BA72] pl-4 text-[#FFE4C4]">Menjelajahi dunia digital satu blok pada satu waktu. Petualangan menanti!</p>

          <div class="flex gap-4 mt-6">
            {#each socialLinks as social}
              {@const Icon = social.icon}
              <a
                href={social.href}
                aria-label={social.label}
                class="w-12 h-12 flex items-center justify-center bg-[#8D6E63] border-[3px] border-[#3E2723]
                          shadow-[4px_4px_0_0_#2E7D32] text-white
                          hover:bg-[#F9BA72] hover:shadow-none hover:-translate-y-2
                          active:translate-y-1
                          transition-all duration-150 group"
              >
                <Icon size={24} strokeWidth={2.5} />
              </a>
            {/each}
          </div>
        </div>

        {#each Object.entries(footerLinks) as [category, links]}
          <div>
            <h3 class="font-bold text-white text-xl mb-6 uppercase tracking-widest border-b-4 border-[#F9BA72] inline-block pb-1 shadow-[2px_2px_0_0_#2E7D32]">
              {category}
            </h3>
            <ul class="space-y-3">
              {#each links as label}
                <li>
                  <!-- svelte-ignore a11y_invalid_attribute -->
                  <a href="#" class="group flex items-center gap-2 font-bold hover:text-white transition-colors duration-100 text-lg">
                    <span class="opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all text-[#F9BA72]">➤</span>
                    <span class="group-hover:animate-pixel-flash">{label}</span>
                  </a>
                </li>
              {/each}
            </ul>
          </div>
        {/each}
      </div>

      <div class="pt-8 border-t-4 border-[#3E2723] flex flex-col md:flex-row justify-between items-center gap-6 text-sm font-bold bg-[#4E342E] -mx-6 px-6 pb-6 shadow-inner">
        <div class="bg-[#3E2723] text-[#F9BA72] px-4 py-2 border-2 border-[#8D6E63]">
          <p>© {currentYear} Pixel Realm. Press Start.</p>
        </div>

        <div class="flex items-center gap-6 text-[#FFE4C4]">
          <div class="flex items-center gap-2 bg-[#3E2723] px-3 py-1 border-2 border-[#8D6E63]">
            <div class="flex gap-1">
              {#each Array(5) as _, i}
                <div class="w-2 h-3 border border-[#8D6E63] {i < 3 ? 'bg-[#41B78E]' : 'bg-[#3E2723]'}"></div>
              {/each}
            </div>
            <span class="uppercase tracking-wider text-xs">HP: OK</span>
          </div>

          <p class="flex items-center gap-1.5 uppercase tracking-wide text-xs">
            Crafted with <Heart size={16} class="text-red-500 fill-red-500 animate-pulse" />
          </p>
        </div>
      </div>
    </div>
  </div>
</footer>

<style>
  .font-pixel {
    font-family: "Pixelify Sans", sans-serif;
  }
  .animate-pulse-slow {
    animation: pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite;
  }

  @keyframes drift {
    from {
      transform: translateX(-100%);
    }
    to {
      transform: translateX(100vw);
    }
  }
  .animate-cloud-drift-slow {
    animation: drift 60s linear infinite;
  }
  .animate-cloud-drift-fast {
    animation: drift 35s linear infinite;
  }

  @keyframes walkAcross {
    from {
      left: -50px;
    }
    to {
      left: 105%;
    }
  }
  .animate-walk-across {
    animation: walkAcross 20s linear infinite;
  }

  @keyframes legWalk {
    0%,
    100% {
      height: 12px;
    }
    50% {
      height: 6px;
    }
  }
  .animate-leg-walk {
    animation: legWalk 0.3s steps(2) infinite alternate;
  }

  @keyframes fadeInUp {
    from {
      opacity: 0;
      transform: translateY(40px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  .animate-fade-in-up {
    animation: fadeInUp 0.8s ease-out forwards;
  }

  @keyframes pixelFlash {
    0%,
    100% {
      color: #ffe4c4;
    }
    50% {
      color: #f9ba72;
      text-shadow: 2px 2px 0px #000;
    }
  }
  .animate-pixel-flash {
    animation: pixelFlash 0.2s steps(2) infinite;
  }

  /* --- BUTTON ANIMATIONS --- */

  /* 1. Glitch */
  @keyframes glitchAnim {
    0% {
      transform: translate(0);
    }
    20% {
      transform: translate(-2px, 2px);
    }
    40% {
      transform: translate(-2px, -2px);
    }
    60% {
      transform: translate(2px, 2px);
    }
    80% {
      transform: translate(2px, -2px);
    }
    100% {
      transform: translate(0);
    }
  }

  .animate-glitch::before,
  .animate-glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #8d6e63; /* Match button background */
  }

  .animate-glitch::before {
    left: 2px;
    text-shadow: -1px 0 #00ffea;
    clip-path: inset(20% 0 30% 0);
    animation: glitchAnim 0.3s infinite linear alternate-reverse;
  }

  .animate-glitch::after {
    left: -2px;
    text-shadow: -1px 0 #ff004c;
    clip-path: inset(50% 0 10% 0);
    animation: glitchAnim 0.3s infinite linear alternate-reverse;
  }

  /* 2. Spin Pixel */
  @keyframes spinPixel {
    0% {
      transform: rotate(0deg);
    }
    25% {
      transform: rotate(90deg);
    }
    50% {
      transform: rotate(180deg);
    }
    75% {
      transform: rotate(270deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  .animate-spin-pixel {
    animation: spinPixel 0.6s steps(4) infinite;
  }

  /* 3. Shine */
  @keyframes shine {
    100% {
      left: 200%;
    }
  }
  .animate-shine {
    animation: shine 0.5s;
  }
</style>
