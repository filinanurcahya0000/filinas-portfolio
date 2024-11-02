<svelte:head>
  <title>Highlight, this is my introduction page!</title>
</svelte:head>

<script>
  import projects from '$lib/projects.json';
  import Project from '$lib/project.svelte';

  // Mock profile data
  let profileData = {
    ok: true,
    json: async () => ({
      followers: 100,
      following: 100,
      public_repos: 100,
      public_gists: 100,
    }),
  };

  // Reactive variables to hold profile data
  let followers, following, public_repos, public_gists;

  // Fetch and display profile data
  $: if (profileData.ok) {
    profileData.json().then(data => {
      followers = data.followers;
      following = data.following;
      public_repos = data.public_repos;
      public_gists = data.public_gists;
    });
  }
</script>

<h1>Filina Nurcahya-Tjoa</h1>
<p>Hi, current data science graduate student at UC San Diego and big data engineer at AT&T.</p>
<img src="images/IMG_1638copy.jpg" alt="This is my favorite mushroom!" height="1000" width="1000">
<p>I currently live in Dallas, TX but what is the fun in that?</p>

<h2>GitHub Profile</h2>
<p>Followers: {followers}</p>
<p>Following: {following}</p>
<p>Public Repos: {public_repos}</p>
<p>Public Gists: {public_gists}</p>

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

  /* Make images responsive and smaller */
  .projects.highlights img {
    max-width: 100%;     /* Scale image to fit within the container */
    height: auto;        /* Maintain aspect ratio */
    object-fit: cover;   /* Crop image to fit within its bounds */
    border-radius: 8px;  /* Optional: rounded corners */
  }

  /* Adjust project container styling */
  .projects.highlights > div {
    padding: 1rem;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Optional: shadow for card effect */
  }
</style>
