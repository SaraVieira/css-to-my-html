<template>
  <div class="wrapper">
    <nuxt/>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css?family=Fira+Sans:300,400');
html {
  font-family: 'Fira Sans', sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  opacity: 0.9;
  background: linear-gradient(to right, #642b73, #c6426e); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  box-shadow: 0 2px 26px 9px rgba(93,101,103,0.10);
  min-height: 100%;
  overflow: hidden;
}

*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
}

.wrapper {
  height: 100vh;
}
</style>
