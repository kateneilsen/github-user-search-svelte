<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let searchFilter = "octocat";
</script>

<div class="search">
  <img class="search-icon" src="assets/icon-search.svg" alt="search" />
  <input
    type="text"
    id="search"
    bind:value={searchFilter}
    placeholder="Search GitHub username..."
  />
  <button class="search" on:click={() => dispatch("filter", searchFilter)}
    >Search</button
  >
</div>
