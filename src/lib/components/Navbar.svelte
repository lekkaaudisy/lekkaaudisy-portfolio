<script lang="ts">
  import { page } from '$app/stores';
  import { fly } from 'svelte/transition';
  import { sineInOut } from 'svelte/easing';

  let siteTitle: string = "Lekka Audisy"; // Customize with your name/brand
  let showMobileMenu: boolean = false;

  const navLinks = [
    { href: '/', label: 'Home' },
    { href: '/about', label: 'About' },
    { href: '/projects', label: 'Projects' },
    { href: '/contact', label: 'Contact' },
    // { href: '/blog', label: 'Blog' }, // Example if you add a blog
  ];

  function toggleMobileMenu() {
    showMobileMenu = !showMobileMenu;
  }

  function closeMobileMenu() {
    showMobileMenu = false;
  }

  // Reactive statement to close mobile menu on route change (if menu is open)
  // This handles cases like browser back/forward or programmatic navigation.
  // The on:click on links is more direct for user actions.
  $: if ($page.url.pathname && showMobileMenu) {
    // This logic might need refinement if it causes unexpected closes.
    // For now, relying on on:click={closeMobileMenu} for explicit user actions.
  }
</script>

<header class="bg-slate-800 dark:bg-slate-900 shadow-md sticky top-0 z-50 transition-colors duration-300">
  <div class="container mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex items-center justify-between h-16 md:h-20">
      <!-- Site Title / Logo -->
      <div class="flex-shrink-0">
        <a href="/" class="text-2xl md:text-3xl font-bold text-white hover:text-sky-400 dark:hover:text-sky-300 transition-colors duration-300">
          {siteTitle}
        </a>
      </div>

      <!-- Desktop Menu -->
      <nav class="hidden md:flex md:items-center md:space-x-1 lg:space-x-2">
        {#each navLinks as link}
          <a
            href={link.href}
            class="px-3 py-2 rounded-md text-sm font-medium transition-all duration-300 ease-in-out group relative"
            class:text-white={$page.url.pathname === link.href}
            class:text-slate-300={$page.url.pathname !== link.href}
            class:hover:text-white={$page.url.pathname !== link.href}
            aria-current={$page.url.pathname === link.href ? 'page' : undefined}
          >
            {link.label}
            <!-- Corrected Underline Span -->
            <span
              class="absolute bottom-0 left-0 block h-0.5 bg-sky-500 max-w-0 group-hover:max-w-full transition-all duration-500 ease-out"
              class:max-w-full={$page.url.pathname === link.href}
            ></span>
          </a>
        {/each}
      </nav>

      <!-- Mobile Menu Button -->
      <div class="md:hidden flex items-center">
        <button
          on:click={toggleMobileMenu}
          type="button"
          class="inline-flex items-center justify-center p-2 rounded-md text-slate-300 hover:text-white hover:bg-slate-700 dark:hover:bg-slate-700 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-sky-500 transition-all duration-300"
          aria-controls="mobile-menu"
          aria-expanded={showMobileMenu}
          aria-label={showMobileMenu ? "Close main menu" : "Open main menu"}
        >
          <span class="sr-only">{showMobileMenu ? "Close main menu" : "Open main menu"}</span>
          {#if showMobileMenu}
            <!-- Close Icon (X) -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 block" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
            </svg>
          {:else}
            <!-- Hamburger Icon -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 block" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          {/if}
        </button>
      </div>
    </div>
  </div>

  <!-- Mobile Menu -->
  {#if showMobileMenu}
    <div
      class="md:hidden fixed inset-x-0 top-16 md:top-20 bg-slate-800 dark:bg-slate-900 shadow-xl z-[60] overflow-y-auto border-t border-slate-700 dark:border-slate-700/50"
      id="mobile-menu"
      transition:fly={{ y: -30, duration: 300, easing: sineInOut }}
    >
      <nav class="px-2 pt-2 pb-4 space-y-1 sm:px-3">
        {#each navLinks as link}
          <a
            href={link.href}
            class="block px-3 py-3 rounded-md text-base font-medium transition-colors duration-200"
            class:bg-sky-600={$page.url.pathname === link.href}
            class:text-white={$page.url.pathname === link.href}
            class:text-slate-200={$page.url.pathname !== link.href}
            class:hover:bg-slate-700={$page.url.pathname !== link.href}
            class:hover:text-white={$page.url.pathname !== link.href}
            aria-current={$page.url.pathname === link.href ? 'page' : undefined}
            on:click={closeMobileMenu}
          >
            {link.label}
          </a>
        {/each}
      </nav>
    </div>
  {/if}
</header>

<style lang="postcss">
  /* Styles for mobile menu scrollability */
  #mobile-menu {
    max-height: calc(100vh - 4rem); /* h-16 for navbar height */
  }
  @media (min-width: 768px) { /* md breakpoint */
    #mobile-menu {
      max-height: calc(100vh - 5rem); /* h-20 for navbar height */
    }
  }
</style>