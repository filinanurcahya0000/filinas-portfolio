<script>
    import { page } from '$app/stores';
    import { base } from '$app/paths';
    import ThemeSwitcher from '$components/ThemeSwitcher.svelte';
    import DataFetcher from '$components/DataFetcher.svelte';
  
    const pages = [
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/", title: "Home" },
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/projects", title: "Projects" },
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/contact", title: "Contact" },
  { url: "https://filinanurcahya0000.github.io/filinas-portfolio/cv", title: "Resume" },
  { url: "https://github.com/filinanurcahya0000/DSC209R-Portfolio", title: "Github" },
];

  
  </script>
  
  <nav>
    {#each pages as p}
      <a
        href={p.url.startsWith('http') ? p.url : `${base}${p.url}`}
        class:current={$page?.url?.pathname === `${base}${p.url}`}
        target={p.url.startsWith('http') ? '_blank' : undefined}
        rel={p.url.startsWith('http') ? 'noopener noreferrer' : undefined}
      >
        {p.title}
      </a>
    {/each}
  </nav>
  
  
  <main>
    <ThemeSwitcher />
    <slot />
    <DataFetcher />
  </main>