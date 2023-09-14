<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let isDarkMode = true;

  import { colorScheme } from "../stores";

  // Set the color scheme each time it changes.
  // Doing it this way could be useful if you use Tailwind with the class strategy.
  $: {
    document.firstElementChild.setAttribute("class", $colorScheme);
    document.firstElementChild.style.colorScheme = $colorScheme;
  }
</script>

<div class="header">
  <h1>devfinder</h1>
  <h6>
    <button
      class="color-scheme {isDarkMode ? 'dark' : ''}"
      on:click={colorScheme.toggle}
    >
      {$colorScheme === "light" ? "Light" : "Dark"}
      <img
        src={$colorScheme === "light"
          ? "assets/icon-sun.svg"
          : "assets/icon-moon.svg"}
        alt={$colorScheme === "light" ? "sun" : "moon"}
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
