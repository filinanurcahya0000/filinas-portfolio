<svelte:head>
  <title>Highlight, this is my introduction page!</title>
</svelte:head>
<script>
    import projects from '$lib/projects.json';
    import project from '$lib/project.svelte';
</script>

<h1> Filina Nurcahya-Tjoa </h1>
<p> Hi, current data science graduate student at UC San Diego and big data engineer at AT&T.</p>
<img src="images/IMG_1638copy.jpg" alt="This is my favorite mushroom!" height="1000" width="1000">
<p>I currently live in Dallas, TX but what is the fun in that? </p>

<h2>Latest Projects</h2>
        <div class="projects highlights">
            {#each projects.slice(0, 3) as project}
                <Project data={project} hLevel={3} />
            {/each}
        </div>
        <style>
            .projects.highlights {
                margin-top: 2rem;
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
                gap: 1rem;
            }
        </style>
