<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
     -->
    <router-view/>
  </div>
</template>

<style lang="scss">
$width-main: 600px;
:root {
    --width-main: #{$width-main};
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
}

a {
    text-decoration: none;
}

ul,
ol {
    list-style: none;
}

#app {
    display: flex;
    flex-direction: column;

    & div {
        display: flex;
        flex-direction: column;

        & .main {
            display: flex;
            margin: auto;
            width: var(--width-main);
        }

        &>.main {
            flex-direction: column;
            padding: 20px 0px;
        }
    }
}
</style>
