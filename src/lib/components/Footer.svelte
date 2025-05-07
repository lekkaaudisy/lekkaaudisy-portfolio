<!-- src/lib/components/Footer.svelte -->
<script lang="ts">
  // Ensure you have lucide-svelte installed: pnpm add lucide-svelte (or npm/yarn)
  import { Github, Linkedin, Mail } from 'lucide-svelte'; // Or other icons you prefer

  const currentYear: number = new Date().getFullYear();
  const yourName: string = "Lekka Audisy"; // Customize with your name

  // Customize these links with your actual profiles and email
  const socialLinks = [
    {
      href: 'https://github.com/lekkaaudisy', // Your GitHub profile URL
      label: 'GitHub',
      icon: Github,
    },
    {
      href: 'https://linkedin.com/in/lekkaaudisy', // Your LinkedIn profile URL
      label: 'LinkedIn',
      icon: Linkedin,
    },
    {
      href: 'mailto:lekkaaudisy@gmail.com', // Your email address
      label: 'Email',
      icon: Mail,
    },
  ];

  const builtWithLinks = [
    { href: 'https://kit.svelte.dev/', label: 'SvelteKit' },
    { href: 'https://tailwindcss.com/', label: 'Tailwind CSS' },
    // { href: 'https://vercel.com/', label: 'Vercel' }, // Example if hosted on Vercel
  ];
</script>

<!--
  Footer with new palette:
  - Background: Consistently dark (slate-800 for light mode, slate-900 or 950 for dark mode)
  - Text: Light muted (slate-400)
  - Link Hovers/Accents: Primary color (sky-400)
-->
<footer class="bg-slate-800 dark:bg-slate-900 border-t border-slate-700 dark:border-slate-700/50 text-slate-400 dark:text-slate-500">
  <!--
    Alternative if you have slate-950 (Tailwind v3.3+): dark:bg-slate-950 for even deeper dark
  -->
  <div class="container mx-auto px-4 sm:px-6 lg:px-8 py-10 md:py-12">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-center text-sm">
      <!-- Copyright & Name -->
      <div class="text-center md:text-left">
        <p>
          © {currentYear} <span class="font-semibold text-slate-300 dark:text-slate-200">{yourName}</span>
        </p>
        <p class="mt-1">All Rights Reserved.</p>
      </div>

      <!-- Social Links -->
      <div class="flex justify-center items-center space-x-5 md:space-x-6">
        {#each socialLinks as social}
          <a
            href={social.href}
            target={social.label === 'Email' ? '_self' : '_blank'}
            rel={social.label === 'Email' ? undefined : 'noopener noreferrer'}
            aria-label={`Connect with ${yourName} on ${social.label}`}
            title={social.label}
            class="text-slate-400 dark:text-slate-500 hover:text-sky-400 dark:hover:text-sky-400 transition-colors duration-300"
          >
            <svelte:component this={social.icon} size={22} stroke-width={1.75} />
            <span class="sr-only">{social.label}</span>
          </a>
        {/each}
      </div>

      <!-- "Built with" - more subtle -->
      <div class="text-center md:text-right text-xs">
        <p>
          Crafted with
          {#each builtWithLinks as link, i}
            <a
              href={link.href}
              target="_blank"
              rel="noopener noreferrer"
              class="font-medium text-slate-400 dark:text-slate-500 hover:text-sky-400 dark:hover:text-sky-400 underline decoration-dotted underline-offset-2 hover:decoration-solid"
            >
              {link.label}
            </a>{#if i < builtWithLinks.length - 1} & {/if}<!--
          -->{/each}.
        </p>
        <!-- Optional: Hosting provider link -->
        <!--
        <p class="mt-1">
          Hosted on <a href="https://[your-host-url.com]" target="_blank" rel="noopener noreferrer" class="font-medium text-slate-400 dark:text-slate-500 hover:text-sky-400 dark:hover:text-sky-400 underline decoration-dotted underline-offset-2 hover:decoration-solid">[Your Host]</a>.
        </p>
        -->
      </div>
    </div>
  </div>
</footer>