<template>
  <div class="app">
    <div id="nav">
      <router-link to="/">Spacer</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,600,700,800,900&display=swap');
  *{
    box-sizing: border-box;
  }

  body {
    font-family: 'Montserrat', Arial, sans-serif;
  }
</style>
