<script>
  import { onMount } from "svelte";
  const base_url = "https://api.github.com/users";
  let user = {};
  let searchFilter = "octocat";
  let date = new Date();
  let day, month, year;

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
    await fetch(`${base_url}/${searchFilter}`)
      .then((response) => response.json())
      .then((data) => {
        user = data;
        date = user.created_at;
      });
  };

  onMount(getUser);
</script>

<main>
  <div class="top-row">
    <h1>devfinder</h1>
    <h6>
      DARK
      <img src="assets/icon-moon.svg" alt="moon" />
    </h6>
  </div>
  <div class="search">
    <img class="search-icon" src="assets/icon-search.svg" alt="search" />
    <input
      type="text"
      id="search"
      bind:value={searchFilter}
      placeholder="Search GitHub username..."
    />
    <button on:click={() => filterUsers()}>Search</button>
  </div>
  <div class="card" id="user">
    <div class="user-top-row">
      <img class="circle" src={user.avatar_url} alt="user avatar" />
      <div class="user-heading">
        <b>{user.name}</b>
        <a href={user.html_url} class="username">@{user.login}</a>
        <p>Joined {joinedOnDate}</p>
      </div>
    </div>

    {#if isAvailable(user.bio)}
      <p>{user.bio}</p>
    {:else}
      <p>Bio Not Available</p>
    {/if}

    <div class="user-github-counts">
      <span class="github-count">
        <p>Repos</p>
        <b>{user.public_repos}</b>
      </span>
      <span class="github-count">
        <p>Followers</p>
        <b>{user.followers}</b>
      </span>
      <span class="github-count">
        <p>Following</p>
        <b>{user.following}</b>
      </span>
    </div>
    <div class="socials">
      <p class={isAvailable(user.location) ? "" : "not-available"}>
        <img src="assets/icon-location.svg" alt="location" />
        {isAvailable(user.location) ? user.location : "Not Available"}
      </p>
      <a href={user.blog} class={isAvailable(user.blog) ? "" : "not-available"}>
        <img src="assets/icon-website.svg" alt="website" />
        {isAvailable(user.blog) ? user.blog : "Not Available"}
      </a>
      <p class={isAvailable(user.twitter_username) ? "" : "not-available"}>
        <img src="assets/icon-twitter.svg" alt="twitter" />
        {isAvailable(user.twitter_username)
          ? user.twitter_username
          : "Not Available"}
      </p>
      <p class={isAvailable(user.company) ? "" : "not-available"}>
        <img src="assets/icon-company.svg" alt="company" />
        {isAvailable(user.company) ? user.company : "Not Available"}
      </p>
    </div>
  </div>
</main>
