<template>
  
     <div class="module-village">
      
        <header>
          <div class="header-background"></div>
          <div id="header-skyeffect">
            <span class="sun"></span>
            <span class="plane"></span>
            <span id="village-pegman">
              <a id="village-pegman-image" href="">Santa Dive</a>
            </span>
          </div>

          <div class="header-content"></div>
        </header>

        <div class="village-body">  
          <div class="ground"></div>
          <div class="road"></div>
          <div class="houses">

              <div id="house-[[item.module]]"
               class$="house [[_calculateHouseClass(item, item.locked, todayHouse)]]">
            <div class="assets housez">
              <div class="building"></div>
              <div class="launchdate" hidden$="[[item.hideDate]]">
                [[_calculateDateNo(item.launchDate)]]
              </div>
              <div class="ice"></div>
            </div>
            
          </div>

          </div>
        </div>

        <div class="countdown-finished"><p hidden="">Come back on the 24th and help us track Santa all night!</p>
            <div class="countdown-test"></div>
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

<style scoped lang="scss">

  $name: 'module-dorf';
  @import '~assets/css/shared/_mixins.scss';
  @import "~assets/css/dorf/_variables.scss";
  @import "~assets/css/dorf/_animations.scss";
  

  $width-big: 600px;
  $toolbar-size: 64px;

  // Moutain screen
  .header-background{
    background-image: url('~assets/images/mountain.svg');
    background-repeat: repeat-x;
    height: 665px;
    width: 100%;
    padding-top: 150px;
    padding-bottom: 200px;
    background-position: 50% 100%;
    background-size: 1618px 791px;
    position: absolute;
    left: 0;
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
      position: absolute;
      top: $sun-top;
      left: 60%;
      width: 107px;
      height: 109px;
      background: url(~assets/images/dorf/sun.svg) no-repeat;
    }

    .plane {
      position: absolute;
      top: $plane-top;
      width: 171px;
      height: 82px;
      margin-left: -(171px/2);
      background: url(~assets/images/dorf/plane.svg) center no-repeat;
      // this only animates across the screen for <10% of the time
      animation: #{$name}-plane 75s infinite linear;
    }

    #village-pegman {
      $img-width: 192px;
      $img-height: 128px;
      transform: translateY(-1000px) translateZ(0);  // hide offscreen
      pointer-events: auto;
      position: absolute;
      overflow: hidden;

      &.fadeout {
        transition: opacity 0.5s;
        opacity: 0;
      }

      #village-pegman-image {
        width: $img-width;
        height: $img-height;
        display: block;
        background: url(~assets/images/dorf/pegman-frames.png);
        background-repeat: no-repeat;
        background-size: $img-width ($img-height * 3);
        font-size: 0;
      }

      left: calc(50% + 520px);

      @media (max-width: ($width-desktop - 1)) {
        top: 20px;
        left: calc(50% + 300px);

        #village-pegman-image {
          transform: scale(0.6);
        }
      }
      @media (max-width: ($width-tablet - 1)) {
        // Land pegman right in the middle of the village, where there's just snow.
        left: calc(50% - 120px);
      }

      &.active {
        animation: 10s #{$name}-skydive ease-in;
        animation-fill-mode: forwards;
        #village-pegman-image {
          animation: 6s #{$name}-skydive-image steps(2);
          animation-delay: 4s;
          animation-fill-mode: both;
        }
      }
    }

  }

  /** Tablet/desktop specific styles. */
  @media (min-width: $width-tablet) {

      .village-body {
        padding-bottom: 500px;

        // Move the village up by 30px, but give the layer an extra 30px to work
        // with: this gives space for the hover cards.
        margin-top: 0 - $village-offset-up - $village-extra-padding;
        padding-top: $village-extra-padding;

        //@import "sass/eastereggs";

        .houses {
          margin: 0 auto;
          width: $width-desktop;
          height: $height-desktop;
          z-index: 10;
        }

        .ground {
          z-index: 1;
          position: absolute;
          background-image: url(~assets/images/dorf/ground.svg);
          background-repeat: repeat-x;
          background-size: $ground-size-w $ground-size-h;
          background-position: 50% 0;
          left:0;
          width: 100%;
          height: 100%;
          top: $ground-top + $village-extra-padding;
        }

        .road {
          position: absolute;
          z-index: 2;
          background-image: url(~assets/images/dorf/road.svg);
          background-repeat: no-repeat;
          background-position: 50% 0;
          background-size: $road-size-w $road-size-h;
          width: 100%;
          height: 100%;
          left:0;
          top: $road-top + $village-extra-padding;
        }

        .house {
          position: relative;
          width: $dim-house;
          height: $dim-house;

          .assets {
            .ice {
              pointer-events: none;
              opacity: 0;
              transition: opacity 2s ease-out;
              //will-change: none;  // don't create a layer; this only transitions once
            }

            .launchdate {
              pointer-events: none;
              position: absolute;
              background: url(~assets/images/dorf/number-bg-dark.svg) center no-repeat;
              background-size: contain;
              transform: translate(-50%, -50%);
              width: 1.6em;
              height: 1.6em;
              font-family: "Lobster";
              font-size: 2.5em;
              color: white;
              display: flex;
              justify-content: center;
              align-items: center;
            }
          }

          &.iced {
            .assets {
              .building {
                a, h3 {
                  display: none;
                }
              }
              .ice {
                opacity: 1;
              }
            }
            h5 {
              display: none;
            }
          }
        }  // .house
      }

      .assets {
        // This is the same size as its parent, but ties in with _houses setting
        // z-index here. This ensures that building/ice is layered correctly with
        // other village things like easter eggs.
        position: absolute;
        width: 100%;
        height: 100%;
      }

      /**
      * Each house's action is basically positioned at its center bottom point,
      * something like its door. The label, e.g. "Play", "Learn" etc is shown
      * just under this point. It provides the base for a touch area.
      */
      .action {
        $size: percent($link-target-size, $dim-house);
        $size-half: percent($link-target-size / 2, $dim-house);

        position: absolute;
        width: $size;
        height: $size;
        margin-bottom: -$size;
        margin-left: -$size-half;

        h5 {
          margin: 0;
          font-size: 12px;
          letter-spacing: 1px;
          font-weight: 600;
          color: #fff;
          line-height: 12px;
          text-transform: uppercase;
          text-align: center;
          color: #37afdb;
          text-shadow: 0 1px 0 rgba(255, 255, 255, 0.125);
          position: relative;  // so .housez class can take effect
        }

        .link {
          // These 100%'s refer to the size of our parent .action.
          width: 100%;
          height: 100%;
          left: 0%;
          bottom: 100%;
          position: absolute;
          z-index: 30000;
          margin-bottom: percent($action-offset-top, $dim-house);

          // Create a layer: this hints to browsers that yes, this card _REALLY IS_
          // above everything else. Since there's no background/color etc, it's
          // ignored anyway.
          //@include will-change();

          $duration-in: 0.23s;
          $easing-in: cubic-bezier(0,1,.33,1.28);
          $duration-out: 0.2s;
          $easing-out: cubic-bezier(.83,.02,1,.01);
          $easing-rotate-in: ease-out;

          .card {
            $hs: $hover-card-size / 2;
            width: $hover-card-size !important;
            height: $hover-card-size !important;
            margin: (-$hs) 0 0 (-$hs);
            //@include will-change(transform, opacity);
            transition: transform $duration-out $easing-out, opacity $duration-out $easing-out;
            transform: scale(0);
            opacity: 0.25;
            left: 50%;
            top: 50%;

            .label {
              display: none;  // hide the 'new' label
            }

            .image {
              border-radius: 10000px;
              box-shadow: 4px 14px 0 rgba(0, 0, 0, .125);
            }

            .launchdate {
              display: none;
            }

            .image {
              transform: rotate(10deg);
              transition: transform .01s ease-out $duration-out;
            }
          }

          // only change state on links with hrefs
          &[href]:hover, &[href]:active {
            .card {
              transition: transform $duration-in $easing-in, opacity $duration-in $easing-in;
              transform: scale(1);
              opacity: 1;

              .image {
                transform: rotate(0deg);
                transition: transform $duration-in $easing-rotate-in .02s;
              }
            }
          }
        }  // .link
      } // .action
    }

    .countdown-finished {
        z-index: 90;
        position: absolute;
        height:350px;
        width: 100%;
        left:0px;
        background: url(https://maps.gstatic.com/mapfiles/santatracker/v201812230903/scenes/dorf/img/footer-snow-tile.svg) repeat-x;
        background-size: contain;
        background-position: center bottom;
      }


    .countdown-test {
        position: absolute;
        left: 300px;
        margin-top: 100px;
        height: 400px;
        width: 1000px;
        max-width: 100%;
        background-image: url(https://maps.gstatic.com/mapfiles/santatracker/v201812230903/scenes/dorf/img/day-of-assets-footer.svg);
        background-size: 100% 100%;
        background-position: top;
      }


</style>
