<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let searchFilter = "octocat";
  export let isDarkMode;
</script>

<div class="search {isDarkMode}">
  <img class="search-icon" src="assets/icon-search.svg" alt="search" />
  <input
    class=" {isDarkMode}"
    type="text"
    id="search"
    bind:value={searchFilter}
    placeholder="Search GitHub username..."
  />
  <button
    class="search-button"
    on:click={() => dispatch("filter", searchFilter)}>Search</button
  >
</div>
