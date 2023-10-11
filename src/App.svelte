<script lang="ts">
  import Counter from './lib/Counter.svelte'
  import { onMount } from "svelte";
  const endpoint = "https://v6.exchangerate-api.com/v6/edd59a2de98f96d5c7c3fd39/latest/RUB";
  let posts = [];

  onMount(async function () {
    const response = await fetch(endpoint);
    const data = await response.json();
    console.log(data);
  });

  export let name:any;
</script>

<main>
  <div>
    <h1>
      Converting app
    </h1>
  </div>

  <div class="card">
    <Counter name={name} />
  </div>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  
</style>
