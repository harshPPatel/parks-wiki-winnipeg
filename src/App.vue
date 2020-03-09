<template>
  <div id="main">
    <router-link to="/" class="logo">
      <i>🏞</i> Parks Wiki <br> <span>WINNIPEG</span>
    </router-link>
    <nav>
      <a href="/about">About</a>
      <a href="https://github.com/harshPPatel/winnipeg-parks-wiki" target="_blank"
        >GitHub
      </a>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
@import './scss/mapbox';
@import './scss/skeleton';

body {
  padding: 0;
  margin: 0;
  font-family: 'Sen', sans-serif;
}

#main {
  width: 100vw;
  min-height: 700px;
  height: 100vh;
  position: relative;

  .logo,
  nav {
    z-index: 999;
    background-color: #fff;
    padding: 10px 20px;
    border-radius: 6px;
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16);
    color: #2e2e2e;

    @media screen and (max-width: 468px) {
      padding: 8px 14px;
    }
  }

  .logo {
    br {
      display: none;
    }

    @media screen and (max-width: 468px) {
      text-align: center;
      br {
        display: block;
      }
    }
    span {
      font-weight: bold;
      font-size: 12px;
      opacity: 0.5;
    }
  }

  nav {
    display: inline-block;
    position: absolute;
    top: 12px;
    right: 20px;

    a {
      color: #2e2e2e;
      font-size: 14px;
      opacity: 1;
      transition: all 0.2s ease;
      &:last-of-type {
        margin-left: 16px;
      }

      &:hover,
      &:active {
        opacity: 0.8;
      }
    }
  }

  .logo:link,
  .logo:visited {
    position: absolute;
    top: 12px;
    left: 20px;
    font-size: 18px;
    font-weight: bold;
    text-decoration: none;
    opacity: 1;
    transition: all 0.2s ease;
  }

  .logo:hover,
  .logo:active {
    text-decoration: underline;
    opacity: 0.85;
  }
}
</style>
