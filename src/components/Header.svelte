<script>
  import { createEventDispatcher } from "svelte";
  import { colorScheme } from "../stores";
  const dispatch = createEventDispatcher();

  export let isDarkMode;
</script>

<div class="header">
  <h1 class=" {isDarkMode}">devfinder</h1>
  <button
    class="color-scheme {isDarkMode}"
    on:click={() => dispatch("toggle", $colorScheme)}
  >
    {$colorScheme == "dark" ? "Light" : "Dark"}
    <img
      src={$colorScheme == "dark"
        ? "assets/icon-sun.svg"
        : "assets/icon-moon.svg"}
      alt={$colorScheme == "dark" ? "sun" : "moon"}
    />
  </button>
</div>
