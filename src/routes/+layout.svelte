<!-- src/routes/+layout.svelte -->
<script lang="ts">
	import '../app.css'; // Your global styles, including Tailwind base/components/utilities
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte';
  
	// If you implement a theme toggle later, you might import a store here
	// import { theme } from '$lib/stores/themeStore'; // Example
	// $: if (typeof document !== 'undefined' && $theme) {
	//   if ($theme === 'dark') {
	//     document.documentElement.classList.add('dark');
	//   } else {
	//     document.documentElement.classList.remove('dark');
	//   }
	// }
  </script>
  
  <!--
	Applying our new color palette:
	- Light Mode Page Background: slate-50 (slightly off-white)
	- Dark Mode Page Background: slate-900 (deep dark)
	- Light Mode Default Text: slate-700 (dark gray for good readability)
	- Dark Mode Default Text: slate-300 (light gray for good readability on dark)
  -->
  <div class="flex min-h-screen flex-col bg-slate-50 text-slate-700 dark:bg-slate-900 dark:text-slate-300 transition-colors duration-300">
	<Navbar />
  
	<main class="flex-grow container mx-auto px-4 py-8 sm:px-6 lg:px-8">
	  <slot />
	</main>
  
	<Footer />
  </div>
  
  <style lang="postcss">
	/* Add any truly global styles here if necessary,
	   but prefer Tailwind utilities or component-specific styles.
	*/
	:global(body) {
	  /* Example: enable smooth scrolling for anchor links across the site */
	  /* scroll-behavior: smooth; */
  
	  /* Improve font rendering (optional, test for preference) */
	  -webkit-font-smoothing: antialiased;
	  -moz-osx-font-smoothing: grayscale;
	}
  </style>