<script>
  import { createEventDispatcher } from "svelte";
  import { colorScheme } from "../stores";
  const dispatch = createEventDispatcher();

  export let isDarkMode;
</script>

<div class="header">
  <h1 class=" {isDarkMode}">devfinder</h1>
  <button
    class="color-scheme"
    on:click={() => dispatch("toggle", $colorScheme)}
  >
    <h6 class=" {isDarkMode}">
      {$colorScheme == "dark" ? "Light" : "Dark"}
    </h6>

    <img
      src={$colorScheme == "dark"
        ? "assets/icon-sun.svg"
        : "assets/icon-moon.svg"}
      alt={$colorScheme == "dark" ? "sun" : "moon"}
    />
  </button>
</div>

<style>
  button {
    display: flex;
    align-items: center;
    gap: 1rem;
    letter-spacing: 2.5px;
  }
</style>
