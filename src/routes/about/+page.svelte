<script lang="ts">
  const yourName: string = "Lekka Audisy"; // Customize if needed elsewhere on this page
</script>

<svelte:head>
  <title>About Me - {yourName}</title>
  <meta name="description" content="Learn more about {yourName}, my journey into web development, and my skills." />
</svelte:head>

<div class="space-y-8">
  <header class="mb-10">
    <h1 class="text-4xl font-bold tracking-tight text-slate-900 dark:text-slate-100 sm:text-5xl">
      A Little More <span class="text-indigo-600 dark:text-indigo-400">About Me</span>
    </h1>
  </header>

  <section class="grid grid-cols-1 md:grid-cols-3 gap-8 items-start">
    <!-- Text Content Column -->
    <div class="md:col-span-2 space-y-6 text-lg text-slate-700 dark:text-slate-300">
      <p>
        [Hello! I'm Lekka Audisy, a passionate and self-motivated web developer based in [Your City/Country, if you want to share]. My journey into the world of code started with [mention your origin story - e.g., a fascination for how websites worked, a specific project idea, a course you took]. I quickly fell in love with the creative process of turning ideas into tangible, interactive digital experiences.]
      </p>
      <p>
        [I thrive on learning new technologies and continuously honing my skills. I'm particularly interested in [mention specific areas like frontend development, backend development, full-stack, UI/UX, specific frameworks like Svelte/React/Vue, etc.]. My goal is to build applications that are not only functional and user-friendly but also aesthetically pleasing and performant.]
      </p>
      <p>
        [When I'm not coding, you might find me [mention a hobby or two, e.g., exploring new tech blogs, contributing to open source, hiking, reading, etc.]. I believe in [mention a core value, e.g., continuous improvement, collaboration, problem-solving].]
      </p>
    </div>

    <!-- Optional Image/Placeholder Column -->
    <div class="md:col-span-1 flex justify-center md:justify-end">
      <!-- Placeholder for an image -->
      <div class="w-48 h-48 sm:w-64 sm:h-64 bg-slate-300 dark:bg-slate-700 rounded-lg flex items-center justify-center text-slate-500 dark:text-slate-400">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1">
          <path stroke-linecap="round" stroke-linejoin="round" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
        </svg>
        <span class="sr-only">Placeholder for my photo</span>
      </div>
      <!--
        When you have a photo:
        <img src="/path/to/your-photo.jpg" alt="A professional photo of {yourName}" class="rounded-lg shadow-lg w-full max-w-xs object-cover" />
        Make sure to put your photo in the `static` folder, e.g., `static/images/profile.jpg` then the src would be `/images/profile.jpg`
      -->
    </div>
  </section>

  <section class="mt-12">
    <h2 class="text-3xl font-semibold mb-6 text-slate-900 dark:text-slate-100">My Core Skills</h2>
    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 text-slate-700 dark:text-slate-300">
      <!-- Example Skills - Customize these! -->
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">JavaScript (ES6+)</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">TypeScript</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">HTML5</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">CSS3 / Tailwind CSS</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">Svelte / SvelteKit</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">Node.js</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">Git / GitHub</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">Responsive Design</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">REST APIs</div>
      <div class="bg-slate-100 dark:bg-slate-800 p-4 rounded-lg shadow">Problem Solving</div>
      <!-- Add more skills as appropriate -->
    </div>
  </section>
</div>