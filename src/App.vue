<template>
  <div id="app">
    <img alt="rHEMote logo" class="logo" src="./assets/logo.png">
    <ComingSoon />
    <RemoteAnimation />
    <!-- TODO: add imprint -->
  </div>
</template>

<script>
import RemoteAnimation from './components/RemoteAnimation.vue';
import ComingSoon from './components/ComingSoon.vue';

export default {
  name: 'app',
  components: {
    ComingSoon,
    RemoteAnimation,
  },
};
</script>

<style lang="less">
@import './assets/less/fonts.less';

body {
  font-family: 'Raleway', Arial, Helvetica, sans-serif;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  .logo {
    max-width: 350px;
    width: 100%;
  }
  button {
    font-family: 'Raleway', Arial, Helvetica, sans-serif;
    &:hover {
      cursor: pointer;
    }
  }
}
</style>
