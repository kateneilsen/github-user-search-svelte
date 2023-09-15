# Frontend Mentor - GitHub user search app solution

This is a solution to the [GitHub user search app challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/github-user-search-app-Q09YOgaH6). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshots](#screenshots)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the app depending on their device's screen size
- See hover states for all interactive elements on the page
- Search for GitHub users by their username
- See relevant user information based on their search
- Switch between light and dark themes
- **Bonus**: Have the correct color scheme chosen for them based on their computer preferences. _Hint_: Research `prefers-color-scheme` in CSS.

### Screenshots

![Mobile: Light](./screenshots/mobile_light.png) <br/>
![Tablet: Dark](./screenshots/tablet_dark.png) <br/>
![Desktop: Light](./screenshots/desktop_light.png)<br/>

### Links

- Solution URL: [https://github.com/kateneilsen/github-user-search-svelte](https://github.com/kateneilsen/github-user-search-svelte)
- Live Site URL: [https://github-user-search-svelte.vercel.app/](https://github-user-search-svelte.vercel.app/)

## My process

### Built with

- [Svelte](https://svelte.dev/) - JS Framework
- JavaScript
- Mobile-first workflow

### What I learned

This is my first project using the svelte framework. I broke the app into 3 components: header, search, and user.
The data request is handled in the parent component(App.svelte)

- Data is shared using props
- svelte has two-way data binding! <br />

**Search.svelte**

```javascript
bind: value = { searchFilter };
```

**App.svelte**

```javascript
bind: searchFilter;
```

- dynamic behavior
- state management

### Continued development

- Svelte stores
- reactivity in svelte
- lifecycles in svelte
- accessibility in svelte

### Useful resources

- [Custom Svelte Store](https://maximmaeder.com/custom-store-for-svelte/) - This helped me with understanding custom stores in svelte and working with the css 'prefers-color-scheme'.
- [MDN: Svelte](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_getting_started) - This is my first project using svelte. I used this article to help me learn the basics and apply them to this project.

## Author

- GitHub - [@kateneilsen](https://www.github.com/kateneilsen)
- Frontend Mentor - [@kateneilsen](https://www.frontendmentor.io/profile/kateneilsen)

**Note: Delete this note and add/remove/edit lines above based on what links you'd like to share.**
