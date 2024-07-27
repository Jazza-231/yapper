<script lang="ts">
  import { browser } from "$app/environment";
  import { onMount } from "svelte";

  let theme: string = "light"; // Default theme

  // Function to apply the current theme
  function applyTheme(currentTheme: string) {
    if (currentTheme === "dark") {
      document.documentElement.classList.add("dark");
    } else {
      document.documentElement.classList.remove("dark");
    }
  }

  // Function to toggle the theme
  function toggle() {
    theme = theme === "dark" ? "light" : "dark";
    localStorage.setItem("theme", theme);
    applyTheme(theme);
  }

  // On component mount, check the stored theme and apply it
  onMount(() => {
    if (browser) {
      const storedTheme = localStorage.getItem("theme");
      if (storedTheme) {
        theme = storedTheme;
        applyTheme(theme);
      } else {
        // Set default theme and apply
        theme = "light";
        localStorage.setItem("theme", theme);
        applyTheme(theme);
      }
    }
  });

  // Export the toggle function so it can be used in the template
  export { toggle };
</script>

<header class="header">
  <div class="container">
    <div class="logo">
      <a href="/">
        <img
          src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/svelte/svelte-plain.svg"
          alt="Svelete Logo"
        />
      </a>
    </div>
    <nav class="nav">
      <ul class="nav-list">
        <li class="nav-item">
          <a href="/" class="nav-link internal-link">Home</a>
        </li>
        <li class="nav-item">
          <a href="/about" class="nav-link internal-link">About</a>
        </li>
        <li class="nav-item">
          <a href="/contact" class="nav-link internal-link">Contact</a>
        </li>
      </ul>
    </nav>
    <div class="right">
      <div class="theme-container">
        <button class="theme-toggle" on:click={toggle}>Theme</button>
      </div>
      <div class="login">
        <a href="/login" class="login-link internal-link">Log In</a>
      </div>
    </div>
  </div>
</header>

<slot></slot>

<footer class="footer">
  <div class="container">
    <div class="footer-top">
      <div class="footer-section footer-about">
        <h2 class="footer-title">About us</h2>
        <p class="footer-text">There is no us. It's just Jazza :D</p>
      </div>
      <div class="footer-section footer-links">
        <h2 class="footer-title">Quick Links</h2>
        <ul class="footer-list">
          <li class="footer-item">
            <a href="/" class="footer-link internal-link">Home</a>
          </li>
          <li class="footer-item">
            <a href="/about" class="footer-link internal-link">About</a>
          </li>
          <li class="footer-item">
            <a href="/contact" class="footer-link internal-link">Contact</a>
          </li>
        </ul>
      </div>
    </div>

    <div class="footer-bottom">
      <p class="footer-copy">&copy; 2024 Jazza. No rights reserved.</p>
    </div>
  </div>
</footer>

<style lang="scss">
  @import "../variables";

  :root {
    --bg: #{$bg-light};
    --icons: #{$icons-light};
    --button-bg: #{$button-bg-light};
    --text: #{$text-light};
    --text-highlight: #{$text-highlight-light};
    --button-active: #{$button-active-light};
    --button-hover: #{$button-hover-light};
    --footer: #{$footer-light};
    --link-internal: #{$link-internal-light};
    --link-external: #{$link-external-light};
    --primary: #{$primary-light};
    --secondary: #{$secondary-light};
    --header-bg: #{$header-bg-light};
    --header-text: #{$header-text-light};
    --header-link: #{$header-link-light};
    --header-link-hover: #{$header-link-hover-light};
    --header-text-hover: #{$header-text-hover-light};
    --filter: invert(1) brightness(0);

    --transition: background-color var(--transition-duration),
      color var(--transition-duration), border-color var(--transition-duration),
      box-shadow var(--transition-duration);

    --transition-duration: 200ms;
    --border-radius: 0.25rem;
  }

  :root.dark {
    --bg: #{$bg-dark};
    --icons: #{$icons-dark};
    --button-bg: #{$button-bg-dark};
    --text: #{$text-dark};
    --text-highlight: #{$text-highlight-dark};
    --button-active: #{$button-active-dark};
    --button-hover: #{$button-hover-dark};
    --footer: #{$footer-dark};
    --link-internal: #{$link-internal-dark};
    --link-external: #{$link-external-dark};
    --primary: #{$primary-dark};
    --secondary: #{$secondary-dark};
    --header-bg: #{$header-bg-dark};
    --header-text: #{$header-text-dark};
    --header-link: #{$header-link-dark};
    --header-link-hover: #{$header-link-hover-dark};
    --header-text-hover: #{$header-text-hover-dark};
    --filter: invert(1);
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
    background-color: var(--bg);
    color: var(--text);
    transition: var(--transition);
  }

  .internal-link {
    padding: 1rem;
    font-size: large;
    text-decoration: none;
    color: var(--text);
    transition: var(--transition);

    &:hover {
      color: var(--link-internal);
    }
  }

  .header {
    .container {
      display: flex;
      width: auto;
      justify-content: space-between;
      align-items: center;
      padding: 1rem;
      background-color: var(--header-bg);
      transition: var(--transition);
      position: relative;

      .nav {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
      }

      .nav-list {
        display: flex;
        list-style-type: none;
        gap: 2rem;
        padding: 0px;
      }

      .logo img {
        transition: var(--transition);
        width: 50px;
        filter: var(--filter);
      }

      .right {
        display: flex;

        .login {
          align-content: center;
        }

        button {
          padding: 1rem;
          font-size: large;
          background-color: var(--button-bg);
          color: var(--text);
          border: none;
          border-radius: var(--border-radius);
          transition: var(--transition);

          &:hover {
            background-color: var(--button-hover);
          }

          &:active {
            background-color: var(--button-active);
          }
        }
      }
    }
  }

  .footer {
    position: fixed;
    bottom: -90px;
    width: 100%;
    background-color: var(--footer);
    transition:
      var(--transition),
      bottom var(--transition-duration);

    &:hover {
      bottom: 0px;
    }

    .container {
      display: flex;
      flex-direction: column;

      .footer-top {
        display: flex;
        justify-content: center;
        gap: 5rem;

        .footer-list {
          display: flex;
          list-style: none;
          padding-left: 0px;

          a {
            padding-left: 0px;
          }
        }
      }

      .footer-bottom {
        display: flex;
        justify-content: center;
        font-size: small;
      }
    }
  }
</style>
