<script lang="ts">
  let name = 'svelte';
  export let count = 0;
  let joke: string | null = null;

  const loadJoke = async () => {
    const res = await fetch('https://icanhazdadjoke.com/', {
      headers: {
        Accept: 'application/json',
      },
    });
    const data = await res.json();
    return data.joke;
  };
</script>

<h1>Hello from {name}!</h1>
<button on:click={() => count += 1}>
  Clicked {count} {count === 1 ? 'time' : 'times'}
</button>

<button on:click={async () => joke = await loadJoke()}>
  Load a {joke !== null ? 'another' : ''} joke
</button>

  
{#if joke !== null}
  <p>{joke}</p>
{/if}
