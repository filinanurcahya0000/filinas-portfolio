<script>
    import { page } from '$app/stores';
    import { onMount } from 'svelte';
  
    const pages = [
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/", title: "Home" },
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/projects", title: "Projects" },
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/contact", title: "Contact" },
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/cv", title: "Resume" },
  { url: "https://github.com/filinanurcahya0000/DSC209R-Portfolio", title: "Github" },
];
    let theme = 'light dark';
  
    function setColorScheme(colorScheme) {
      if (typeof document !== 'undefined') {
        document.documentElement.style.setProperty('color-scheme', colorScheme);
        if (colorScheme === "dark") {
          document.body.classList.add("dark-mode");
        } else {
          document.body.classList.remove("dark-mode");
        }
        localStorage.colorScheme = colorScheme;
      }
    }
  
    onMount(() => {
      if ("colorScheme" in localStorage) {
        theme = localStorage.colorScheme;
        setColorScheme(theme);
      } else if (typeof window !== 'undefined') {
        const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)").matches;
        setColorScheme(prefersDarkScheme ? "dark" : "light");
      }
    });
  </script>
  
  <nav>
    {#each pages as p}
      <a
        href={p.url}
        class:current={$page.url.pathname === p.url}
        target={p.url.startsWith('http') ? '_blank' : undefined}
      >
        {p.title}
      </a>
    {/each}
  </nav>
  
  <label class="color-scheme">
    Theme:
    <select bind:value={theme} on:change={(e) => setColorScheme(e.target.value)}>
      <option value="light dark">Automatic</option>
      <option value="light">Light</option>
      <option value="dark">Dark</option>
    </select>
  </label>
  
  <main>
    <slot />
  </main>
  