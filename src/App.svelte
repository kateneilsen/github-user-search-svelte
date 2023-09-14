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

  const filterUsers = async () => {
    await fetch(`${base_url}/${searchFilter}`)
      .then((response) => response.json())
      .then((data) => {
        user = data;
        date = user.created_at;
      });
  };

  const joinedOnDate = date.toLocaleDateString("en-US", {
    day: "numeric",
    month: "short",
    year: "numeric",
  });

  const isAvailable = (value) => {
    if (value === "" || value === null || value === undefined) {
      return false;
    }
    return true;
  };

  const getUser = async () => {
    console.log(searchFilter);
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

  // Set the color scheme each time it changes.
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
  <Search {isDarkMode} bind:searchFilter on:filter={() => filterUsers()} />
  <User {user} {joinedOnDate} {isDarkMode} />
</main>
