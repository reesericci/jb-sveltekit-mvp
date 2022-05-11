<script>
  import {page} from '$app/stores';
  import { onMount } from "svelte"
  
  const show = $page.stuff.show
  
  const episode = $page.stuff.episode
  
  let hosts = []
  
  onMount(() => {
    episode.hosts.forEach(async (host) => {

      const res = await fetch(`/hosts/${host}.json`)
      const req = await res.json()
      
      hosts = [...hosts,req.name]
  
    })
  
  })
</script>

<header>
<h1>{show.name} {episode.number}: {episode.title}</h1>
<h3>Hosted by: {#each hosts as host}<span>{host} </span>{/each}</h3>
<div>
  {#each episode.tags as tag}
    <span class="tag">
      {tag}
    </span>
  {/each}
  
</div>
  
</header>


<slot></slot>

<style>
  :global(sponsor) {
    padding: 0.25rem 1rem 0.25rem 1rem;
    background-color: lightgreen;
    display: block;
    margin: 1rem 0 1rem 0;
    max-width: 50rem;
    color: black;
  }
  
  :global(sponsor > ul > li > a) {
    color: blue;
  }
  
  :global(sponsor > h2) {
    margin-top: 1rem;
    margin-bottom: 1rem;
    font-size: 1.5rem;
  }
  
  :global(sponsor > ul > li) {
    font-size: 1rem;
  } 
  
  .tag {
    padding: 0.25rem;
    background-color: lightgrey;
    margin-right: 0.25rem;
    color: black;
  }
  
  header {
    margin-bottom: 2rem;
  }
  
  :global(li) {
    padding: 0.25rem;
  }
</style>
