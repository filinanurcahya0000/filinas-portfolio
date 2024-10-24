      
<svelte:head>
    <title>This is my projects!</title>
</svelte:head>

<script> import projects from '$lib/projects.json' ;</script>
<pre>{ JSON.stringify(projects, null, "\t") }</pre>

   <h1>This is my projects page! { projects.length }</h1> 

    <div class="projects">
        {#each projects as p}
        <article>
            <h2>Lorem ipsum dolor sit.</h2>
            <img src="https://vis-society.github.io/labs/2/images/empty.svg" alt="" />
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Magnam dolor quos,
              quod assumenda explicabo odio, nobis ipsa laudantium quas eum veritatis
              ullam sint porro minima modi molestias doloribus cumque odit.
            </p>
          </article>
          {/each}
    </div>
