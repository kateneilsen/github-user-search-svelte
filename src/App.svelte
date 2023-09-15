<script>
  import { onMount } from "svelte";
  import Header from "./components/Header.svelte";
  import Search from "./components/Search.svelte";
  import User from "./components/User.svelte";
  const base_url = "https://api.github.com/users";

  import { colorScheme } from "./stores";
  $: isDarkMode = $colorScheme === "dark" ? "dark" : "";

  let user = {};
  let searchFilter = "";
  let searchError = false;

  $: {
    if ($colorScheme === "dark") {
      document.body.classList.add("dark");
    } else {
      document.body.classList.remove("dark");
    }
  }

  const getUser = async () => {
    if (searchFilter === "") {
      const data = await fetch(`${base_url}/octocat`);
      const result = await data.json();
      user = result;
    } else {
      const data = await fetch(`${base_url}/${searchFilter}`);
      if (data.status === 404) {
        searchError = true;
        searchFilter = "";
      } else {
        searchError = false;
        const result = await data.json();
        user = result;
      }
    }
  };

  onMount(async () => await getUser());
</script>

<main>
  <Header {isDarkMode} on:toggle={() => colorScheme.toggle()} />
  <Search
    {isDarkMode}
    bind:searchFilter
    on:filter={() => getUser()}
    {searchError}
  />
  <User {user} {isDarkMode} />
</main>
