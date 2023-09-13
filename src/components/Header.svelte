<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let isDarkMode = true;
</script>

<div class="header">
  <h1>devfinder</h1>
  <h6>
    <button
      class="color-scheme {isDarkMode ? 'dark' : ''}"
      on:click={() => (isDarkMode = !isDarkMode)}
    >
      {isDarkMode ? "Light" : "Dark"}
      <img
        src={isDarkMode ? "assets/icon-sun.svg" : "assets/icon-moon.svg"}
        alt={isDarkMode ? "sun" : "moon"}
      />
    </button>
  </h6>
</div>

<style>
  button.color-scheme {
    display: flex;
    align-items: center;
    gap: 1rem;
    letter-spacing: 2.5px;
  }
</style>
