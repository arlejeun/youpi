<template>
  
     <div id="village-all">
       <div id="background"></div>
       <div id="eastereggs">
         <div id="easteregg-tree"></div>
         <div id="easteregg-blocks"></div>
         <div id="easteregg-statue"></div>
         <div id="easteregg-penguin-revolt"></div>
        </div>
      </div>

</template>

<script>

export default {
  components: {

  }
}
</script>

<style lang="scss">

$name: 'module-dorf';
@import "~assets/css/dorf/_variables.scss";
@import "~assets/css/dorf/_animations.scss";


#village-all {
  width: 100%;
  height: 100%;
  left:0px;
  top:0px;
  background-color:#f5f2e2;
  font-size: 12px;
  pointer-events: none;
  padding-bottom: 300px;
  margin-top: -110px;
  border-top: 80px solid transparent;
}

#village-all #background{
    background-image: url('~assets/images/dorf/ground.svg');
    position: fixed;
    overflow-y: scroll;
    max-height: 100%;
    top: 50px;
    left: 0;
    right: 0;
    height: 2937.8px;
    background-repeat: repeat-x;
    background-size: 2815.2px 2752.8px;
}

#village-all #background::after{
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2551.6px;
    background-image: url(~assets/images/dorf/road.svg);
    background-repeat: no-repeat;
}

</style>
