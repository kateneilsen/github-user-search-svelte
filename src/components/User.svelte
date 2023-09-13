<script>
  export let user = {};
  export let joinedOnDate;

  const isAvailable = (value) => {
    if (value === "" || value === null || value === undefined) {
      return false;
    }
    return true;
  };
</script>

<div class="card" id="user">
  <div class="card-header">
    <img class="circle" src={user.avatar_url} alt="user avatar" />
    <div class="header-info">
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
