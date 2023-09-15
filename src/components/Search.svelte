<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let searchFilter = "octocat";
  export let isDarkMode;
  export let searchError = false;
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
  <b class="error {searchError ? 'show' : ''}">No Results</b>
  <button
    class="search-button"
    on:click={() => dispatch("filter", searchFilter)}
    on:on:keydown={() => dispatch("filter", searchFilter)}>Search</button
  >
</div>

<style>
  b.error {
    display: none;
    color: red;
    font-size: 10px;
    align-items: center;
    justify-content: flex-end;
    width: 30%;
    flex-direction: row;
  }
  b.error.show {
    display: flex;
  }
</style>
