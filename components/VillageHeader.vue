<template>
  
     <div class="village-header">
          <div class="moutain"></div>
         <!-- <v-img gradient class="moutain"></v-img>-->
          <div id="header-skyeffect">
            <span class="sun"></span>
            <span class="plane"></span>
            <span id="village-pegman">
              <a id="village-pegman-image" href="/intro">Santa Dive</a>
            </span>
          </div>
      </div>

  
      
    
</template>

<script>
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {

    VuetifyLogo
  }
}
</script>

<style lang="scss">

  $name: 'module-dorf';

  @import "~assets/css/dorf/_variables.scss";
  @import "~assets/css/dorf/_animations.scss";


  .village-header {
    width: 100%;
    height: 100%;
    position:fixed;
    left:0px;

  }

  .village-header .moutain{
    background-image: url('~assets/images/mountain.svg');
    background-repeat: repeat-x;
    width: 100%;
    height: 100%;
    background-size: 70%;
    background-position: top;
  }

/** Contains all effects, like snow, the airplane etc. */
    #header-skyeffect {
      z-index: $base-raised-z-index;
      position: absolute;
      width: 100%;
      height: 630px;
      overflow: hidden;

      santa-weather {
        height: 100%;
      }

      span {
        display: inline-block;
        position: absolute;
      }

      .sun {
        position: fixed;
        top: 32px;
        left: 70%;
        width: 107px;
        height: 109px;
        background: url('~assets/images/dorf/sun.svg') no-repeat;
      }

      .plane {
        position: fixed;
        top: 32px;
        width: 171px;
        height: 82px;
        margin-left: -(171px/2);
        background: url('~assets/images/dorf/plane.svg') center no-repeat;
        // this only animates across the screen for <10% of the time
        animation: #{$name}-plane 75s infinite linear;
      }

      
    }


</style>
