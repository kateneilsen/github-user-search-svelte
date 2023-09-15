<script>
  export let user = {};
  $: joinedOn = new Date(user.created_at).toLocaleDateString("en-US", {
    month: "short",
    day: "numeric",
    year: "numeric",
  });

  const isAvailable = (value) => {
    if (value === "" || value === null || value === undefined) {
      return false;
    }
    return true;
  };

  export let isDarkMode;
</script>

<div class="card {isDarkMode}">
  <div class="header-info">
    <img class="circle" src={user.avatar_url} alt="user avatar" />
    <span class="header-text">
      <b class=" {isDarkMode}">{user.name}</b>
      <a href={user.html_url} class="username">@{user.login}</a>
      <p class=" {isDarkMode}">
        Joined {joinedOn}
      </p>
    </span>
  </div>

  {#if isAvailable(user.bio)}
    <p class=" {isDarkMode}">{user.bio}</p>
  {:else}
    <p class="bio">Bio Not Available</p>
  {/if}

  <div class="user-github-counts {isDarkMode}">
    <span class="github-count {isDarkMode}">
      <p>Repos</p>
      <b>{user.public_repos}</b>
    </span>
    <span class="github-count {isDarkMode}">
      <p class=" {isDarkMode}">Followers</p>
      <b class=" {isDarkMode}">{user.followers}</b>
    </span>
    <span class="github-count {isDarkMode}">
      <p class=" {isDarkMode}">Following</p>
      <b>{user.following}</b>
    </span>
  </div>
  <div class="socials">
    <p class={isAvailable(user.location) ? "" : "not-available"}>
      <img src="assets/icon-location.svg" alt="location" />
      {isAvailable(user.location) ? user.location : "Not Available"}
    </p>
    <a
      href={user.blog}
      class={isAvailable(user.blog) ? isDarkMode : "not-available"}
    >
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
