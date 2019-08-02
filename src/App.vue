<template>
  <div id="app">
    <section>
      <img alt="rHEMote logo" class="logo" src="./assets/logo.png">
      <ComingSoon />
      <RemoteAnimation />
      <a @click="goToImprint" class="imprint-link" href="#">Imprint</a>
    </section>
    <Imprint class="imprint" :style="{ height: imprintHeight + 'px' }" />
  </div>
</template>

<script>
import RemoteAnimation from './components/RemoteAnimation.vue';
import ComingSoon from './components/ComingSoon.vue';
import Imprint from './components/Imprint.vue';

export default {
  name: 'app',
  data() {
    return {
      imprintHeight: 0,
    };
  },
  components: {
    ComingSoon,
    RemoteAnimation,
    Imprint,
  },
  methods: {
    goToImprint(e) {
      this.imprintHeight = (this.imprintHeight > 0) ? 0 : 400;
      e.preventDefault();
      const { scrollHeight } = this.$el.querySelector('section');
      setTimeout(() => {
        window.scrollTo({ top: scrollHeight, left: 0, behavior: 'smooth' });
      }, 300);
    },
  },
};
</script>

<style lang="less">
  @import './assets/less/fonts.less';

  body {
    font-family: 'Raleway', Arial, Helvetica, sans-serif;
    margin: 0;
    padding: 0;
  }

  #app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    .logo {
      max-width: 350px;
      width: 100%;
      margin-top: 60px;
    }
    button {
      font-family: 'Raleway', Arial, Helvetica, sans-serif;
      &:hover {
        cursor: pointer;
      }
    }
  }

  section {
    height: 100vh;
  }

  .imprint-link {
    position: absolute;
    bottom: 10px;
    display: block;
    width: 100px;
    left: 50%;
    margin-left: -50px;
    text-align: center;
    background: gray;
    border-radius: 5%;
    padding: 5px;
    box-sizing: border-box;
    color: #fff;
    text-decoration: none;
  }

  .imprint {
    overflow: hidden;
    transition: height .3s ease-in-out;
  }

</style>
