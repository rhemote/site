<template>
  <div>
    <!-- TODO: make it responsive -->
    <div id="animation-wrapper" :class="{active: isActive}">

      <Phone />

      <Connection position="first" />

      <Connection position="fourth" />

      <Server />

      <Connection position="second" />

      <Connection position="third" />

      <Lamp />

      <button class="play" @click="play">Play</button>
    </div>

    <!-- <button @click="reset" style="top: 25px; position: absolute; left: 10px;">Clear</button> -->

  </div>
</template>

<script>
import Connection from './images/Connection.vue';
import Lamp from './images/Lamp.vue';
import Phone from './images/Phone.vue';
import Server from './images/Server.vue';

export default {
  components: {
    Connection,
    Lamp,
    Phone,
    Server,
  },
  data() {
    return {
      isActive: false,
    };
  },
  methods: {
    reset() {
      console.log('reset');
      this.isActive = !this.isActive;
    },
    play() {
      console.log('play');
      if (!this.isActive) {
        this.isActive = !this.isActive;
        setTimeout(() => {
          this.reset();
        }, 6000);
      }
    },
  },
};
</script>

// TODO: move styles to components
<style lang="less">
  // Step 1 Phone Color
  @step-1-duration: .5s;
  @step-1-delay: .2s;

  // Step 2 Connection First
  @step-2-duration: .7s;
  @step-2-delay: @step-1-duration + @step-1-delay;

  // Step 3 Server Lamp
  @step-3-duration: .5s;
  @step-3-delay: @step-2-duration + @step-2-delay;

  // Step 4 Connection Second
  @step-4-duration: .7s;
  @step-4-delay: @step-3-duration + @step-3-delay;

  // Step 5 Lamp
  @step-5-duration: .3s;
  @step-5-delay: @step-4-duration + @step-4-delay;

  // Step 6 Lamp Stripes
  @step-6-duration: .3s;
  @step-6-delay: @step-5-duration + @step-5-delay;

  // Step 7 Connection Third
  @step-7-duration: .7s;
  @step-7-delay: @step-6-duration + @step-6-delay;

  // Step 8 Connection Fourth
  @step-8-duration: .7s;
  @step-8-delay: @step-7-duration + @step-7-delay;

  // Step 9 Phone Color Second
  @step-9-duration: .5s;
  @step-9-delay: @step-8-duration + @step-8-delay;

  @connection-width: 235px;

  .phone,
  .server,
  .lamp,
  .connection,
  .play {
    position: absolute;
    top: 0;
    left: 0;
  }

  .play {
    top: 235px;
    left: 385px;
    position: absolute;
    color: #494949;
    text-transform: uppercase;
    text-decoration: none;
    background: #ffffff;
    padding: 20px;
    border: 4px solid #494949;
    display: inline-block;
    transition: all 0.4s ease 0s;
    &:hover {
      color: #ffffff;
      background: #009245;
      border-color: #009245;
      transition: all 0.4s ease 0s;
    }
  }

  .phone {
    left: 50px;
    top: 200px;
    svg {
      height: 150px;
      #row-3 {
        fill: #CCCCCC;
        // Step 1
        transition: fill @step-1-duration ease-in-out @step-1-delay;
      }
      #row-3-2 {
        fill: transparent;
        // Step 9
        transition: fill 0.5s ease-in-out 0.5s;
      }
    }
  }

  .server {
    left: 360px;
    top: 50px;
    svg {
      height: 50px;
      #lamp-1 {
        fill: #666;
        transition: fill 0.5s ease-in-out 0.5s;
      }
    }
  }

  .lamp {
    left: 680px;
    top: 170px;
    svg {
      height: 150px;
      #lamp-glass {
        fill: #f2f2f2;
        transition: fill 0.5s ease-in-out 0.5s;
      }
      each(range(7), {
        #stripe-@{value} {
          fill: transparent;
          transition: fill 0.5s ease-in-out 0.5s;
        }
      });
    }
  }

  .connection {
    width: 0px;
    height: 15px;
    overflow: hidden;
    transform-origin: left;
    transition: width .5s linear .5s;
    &.first {
      top: 190px;
      left: 140px;
      transform: rotateZ(-30deg);
    }
    &.second {
      top: 70px;
      left: 495px;
      transform: rotateZ(30deg);
    }
    &.third {
      top: 200px;
      left: 695px;
      transform: rotateZ(210deg);
    }
    &.fourth {
      top: 83px;
      left: 348px;
      transform: rotateZ(-210deg);
    }
    svg {
      width: @connection-width;
      height: 10px;
      stroke-width: 5px;
      stroke-dasharray: 5;
      animation: dash .6s linear infinite;
    }
  }

  #animation-wrapper {
    position: relative;
    margin: 0 auto;
    max-width: 860px;
    width: 100%;
    padding-bottom: 35%;
    &.active {
      .phone {
        svg {
          #row-3 {
            fill: red;
          }
          #row-3-2 {
            fill: #1BDF21;
            transition: fill @step-9-duration ease-in-out @step-9-delay;
          }
        }
      }
      .server {
        svg {
          #lamp-1 {
            fill: orange;
            // Step 3
            transition: fill @step-3-duration ease-in-out @step-3-delay;
          }
        }
      }
      .lamp {
        svg {
          each(range(7), {
            #stripe-@{value} {
              fill: #FFBA42;
              // Step 6
              transition: fill @step-6-duration ease-in-out @step-6-delay;
            }
          });
        }
        #lamp-glass {
          fill: #FFBA42;
          // Step 5
          transition: fill @step-5-duration ease-in-out @step-5-delay;
        }
      }
      .connection {
        width: @connection-width;
        &.first {
          // Step 2
          transition: width @step-2-duration linear @step-2-delay;
        }
        &.second {
          // Step 4
          transition: width @step-4-duration linear @step-4-delay;
        }
        &.third {
          // Step 7
          transition: width @step-7-duration linear @step-7-delay;
        }
        &.fourth {
          // Step 8
          transition: width @step-8-duration linear @step-8-delay;
        }
      }
    }
  }

  @keyframes dash {
    to {
      stroke-dashoffset: -10;
    }
  }
</style>
