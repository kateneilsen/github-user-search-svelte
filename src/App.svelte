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
  let date = new Date();
  let searchError = false;

  const filterUsers = async () => {
    try {
      const response = await fetch(`${base_url}/${searchFilter}`);
    } catch (error) {
      searchError = true;
      console.log(error);
      return;
    }
    user = data;
    date = user.created_at;
  };

  const joinedOnDate = date.toLocaleDateString("en-US", {
    day: "numeric",
    month: "short",
    year: "numeric",
  });

  const getUser = async () => {
    if (searchFilter === "") {
      await fetch(`${base_url}/octocat`)
        .then((response) => response.json())
        .then((data) => {
          user = data;
          date = user.created_at;
        });
    } else {
      await fetch(`${base_url}/${searchFilter}`)
        .then((response) => response.json())
        .then((data) => {
          user = data;
          date = user.created_at;
        });
    }
  };

  $: {
    if ($colorScheme === "dark") {
      document.body.classList.add("dark");
    } else {
      document.body.classList.remove("dark");
    }
  }
  onMount(getUser);
</script>

<main>
  <Header {isDarkMode} on:toggle={() => colorScheme.toggle()} />
  <Search
    {isDarkMode}
    bind:searchFilter
    on:filter={() => filterUsers()}
    {searchError}
  />
  <User {user} {joinedOnDate} {isDarkMode} />
</main>
