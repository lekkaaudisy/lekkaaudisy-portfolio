<!-- src/routes/+page.svelte -->
<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  import { sineInOut } from 'svelte/easing';
  import { fly, fade } from 'svelte/transition';

  // Icons from lucide-svelte for the "What I Do" section
  // Ensure these match the icons used in your expertiseData
  import { MonitorSmartphone, ServerCog, Palette, Layers, CodeXml, DatabaseZap, Users } from 'lucide-svelte';

  // --- Hero Content & Logic ---
  let name: string = "Lekka Audisy"; // Customize
  let titles: string[] = [
    "Web Developer",
    "SvelteKit Specialist",
    "UI/UX Enthusiast",
    "Creative Problem Solver",
    "Digital Craftsman"
  ]; // Customize these titles
  let currentTitleIndex: number = 0;
  let displayedTitle: string = "";
  let titleInterval: any;

  function typeTitle(title: string, onComplete: () => void) {
    let i = 0;
    displayedTitle = "";
    const typingSpeed = 100; // ms
    function typeChar() {
      if (i < title.length) {
        displayedTitle += title.charAt(i);
        i++;
        setTimeout(typeChar, typingSpeed);
      } else {
        setTimeout(onComplete, 1500); // Pause before erasing
      }
    }
    typeChar();
  }

  function eraseTitle(onComplete: () => void) {
    let i = displayedTitle.length;
    const erasingSpeed = 60; // ms
    function eraseChar() {
      if (i > 0) {
        displayedTitle = displayedTitle.substring(0, i - 1);
        i--;
        setTimeout(eraseChar, erasingSpeed);
      } else {
        onComplete();
      }
    }
    eraseChar();
  }

  function cycleTitles() {
    eraseTitle(() => {
      currentTitleIndex = (currentTitleIndex + 1) % titles.length;
      typeTitle(titles[currentTitleIndex], cycleTitles);
    });
  }

  let loaded: boolean = false; // For hero fade-in

  onMount(() => {
    loaded = true;
    typeTitle(titles[currentTitleIndex], cycleTitles); // Start title cycling for hero
    return () => {
      clearInterval(titleInterval); // Cleanup interval on component destroy
    };
  });

  // --- Data for Expertise Cards ---
  // CRITICAL: Customize this array with your actual skills, descriptions, and chosen Lucide icons
  const expertiseData = [
    {
      icon: MonitorSmartphone, // Or CodeXml
      title: "Frontend Development",
      description: "Crafting intuitive, responsive, and high-performance user interfaces with SvelteKit, TypeScript, and modern CSS. Passionate about pixel-perfect execution and accessibility."
    },
    {
      icon: ServerCog, // Or DatabaseZap
      title: "Backend & APIs",
      description: "Building robust server-side logic and scalable RESTful APIs using Node.js & Express. Experienced with database design and integration (e.g., PostgreSQL, MongoDB)."
    },
    {
      icon: Palette, // Or Users
      title: "UI/UX & Prototyping",
      description: "Designing user-centric experiences from wireframes to interactive prototypes using Figma. Focused on creating interfaces that are both beautiful and easy to use."
    },
    // Example of a fourth card if you want to add more:
    // {
    //   icon: Layers,
    //   title: "Full-Stack Solutions",
    //   description: "Delivering end-to-end web applications by seamlessly integrating frontend and backend technologies, ensuring a cohesive and efficient user experience."
    // }
  ];

</script>

<svelte:head>
  <title>{name} - Web Developer Portfolio</title>
  <meta name="description" content="The portfolio of {name}, a creative web developer specializing in SvelteKit, Node.js, and modern UI/UX design." />
</svelte:head>

<!-- Hero Section with new palette -->
<section class="relative flex flex-col items-center justify-center min-h-screen text-center text-white overflow-hidden px-4 py-16 sm:py-24 bg-slate-900">
  <!-- Animated Gradient Background -->
  <div class="absolute inset-0 -z-10 opacity-90">
    <div class="animated-gradient h-full w-full"></div>
  </div>

  <!-- Content Container -->
  <div
    class="relative z-10 transition-opacity duration-1000 ease-in-out"
    class:opacity-0={!loaded}
    class:opacity-100={loaded}
  >
    {#if loaded}
      <div in:fly={{ y: 50, duration: 800, easing: sineInOut, delay: 200 }}>
        <h1 class="text-5xl font-extrabold tracking-tight text-white sm:text-6xl md:text-7xl lg:text-8xl">
          <span class="block">Hi, I'm</span>
          <!-- Using sky-300 (our primary accent) for the name -->
          <span class="block text-sky-300 hover:text-sky-200 transition-colors mt-2 sm:mt-4">{name}</span>
        </h1>
      </div>

      <div in:fly={{ y: 50, duration: 800, easing: sineInOut, delay: 500 }}>
        <p class="mt-6 text-xl sm:text-2xl md:text-3xl font-medium text-slate-200 min-h-[3em] sm:min-h-[2.5em]">
          I'm a <span class="font-bold text-white">{displayedTitle}</span><span class="cursor-blink">|</span>
        </p>
      </div>

      <div in:fly={{ y: 50, duration: 800, easing: sineInOut, delay: 800 }} class="mt-10 sm:mt-12">
        <p class="max-w-xl mx-auto text-lg text-slate-300 sm:text-xl md:max-w-2xl">
          I craft beautiful, responsive, and performant web experiences that users love.
          Let's build something amazing together.
        </p>
      </div>

      <div in:fade={{ duration: 800, delay: 1200 }} class="mt-10 sm:mt-12 flex flex-col sm:flex-row items-center justify-center gap-4">
        <!-- Primary Button using sky-500 -->
        <a
          href="/projects"
          class="w-full sm:w-auto inline-flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-sky-500 hover:bg-sky-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-slate-900 focus:ring-sky-400 md:py-4 md:text-lg md:px-10 transform transition-all hover:scale-105 duration-300 shadow-lg"
        >
          View My Work
        </a>
        <!-- Secondary/Outlined Button using sky accent -->
        <a
          href="/contact"
          class="w-full sm:w-auto inline-flex items-center justify-center px-8 py-3 border border-sky-400 text-base font-medium rounded-md text-white hover:bg-sky-500 hover:bg-opacity-20 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-slate-900 focus:ring-sky-400 md:py-4 md:text-lg md:px-10 transform transition-all hover:scale-105 duration-300"
        >
          Get In Touch
        </a>
      </div>
    {/if}
  </div>

  {#if loaded}
    <div
      in:fade={{ duration: 1000, delay: 2000 }}
      class="absolute bottom-10 left-1/2 -translate-x-1/2 z-10"
    >
      <a href="#what-i-do" aria-label="Scroll down">
        <svg class="w-8 h-8 text-sky-300 hover:text-white transition-colors animate-bounce" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
          <path d="M19 9l-7 7-7-7"></path>
        </svg>
      </a>
    </div>
  {/if}
</section>

<!-- What I Do / My Expertise Section with new palette -->
<section id="what-i-do" class="py-16 md:py-24 bg-slate-100 dark:bg-slate-800">
  <div class="container mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-12 md:mb-16">
      <h2 class="text-3xl font-extrabold text-slate-900 dark:text-slate-50 sm:text-4xl lg:text-5xl">
        My Core <span class="text-sky-500 dark:text-sky-400">Expertise</span> <!-- Primary accent -->
      </h2>
      <p class="mt-4 text-lg md:text-xl text-slate-600 dark:text-slate-300 max-w-2xl mx-auto">
        I specialize in crafting modern, responsive, and user-centric web applications from concept to deployment.
      </p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      {#each expertiseData as item}
        <div class="bg-white dark:bg-slate-900 p-6 rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-[1.01]">
          <div class="flex items-center justify-center w-12 h-12 bg-sky-100 dark:bg-sky-500/10 ring-1 ring-sky-500/20 rounded-full mb-6 text-sky-600 dark:text-sky-400"> <!-- Icon container & icon color (primary) -->
            <svelte:component this={item.icon} size={28} stroke-width={1.5} />
          </div>
          <h3 class="text-xl font-semibold text-slate-900 dark:text-white mb-3">
            {item.title}
          </h3>
          <p class="text-slate-700 dark:text-slate-400 text-sm leading-relaxed">
            {item.description}
          </p>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Add more sections below as needed, e.g., Featured Projects, Testimonials, Contact CTA -->

<style lang="postcss">
  .animated-gradient {
    /* Gradient using shades of sky blue for a cohesive feel with the primary color */
    background: linear-gradient(-45deg, #0c4a6e, #0369a1, #0ea5e9, #38bdf8); /* Tailwind sky-900, sky-700, sky-500, sky-400 */
    background-size: 400% 400%;
    animation: gradientBG 20s ease infinite;
  }

  @keyframes gradientBG {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  .cursor-blink {
    animation: blink 1s step-end infinite;
  }

  @keyframes blink {
    from, to { opacity: 1; }
    50% { opacity: 0; }
  }

  section:first-of-type { /* Targets the Hero section */
    min-height: 100vh;
    min-height: 100svh;
  }
</style>