<template>
<!--create svg 100 wide and 100 high-->
  <!--<svg id="viewport" :height="viewHeight" :width="viewWidth">
    <polygon @click="test()" v-for="element in elements" v-bind:points="ComplilePointsString(element.depth, element.frontDiameter, element.backDiameter, element.frontRadius, element.backRadius, element.x, element.y)" style="fill:aqua;stroke:purple;stroke-width:0.3"/>
  </svg>-->

  <Viewport id="viewport" :elements="elements"/>
</template>

<script>
import Viewport from './components/Viewport.vue';

export default {
    name: "App",
    data() {
        return {
            elements: {
                element1: {
                    depth: 75,
                    frontDiameter: 200,
                    backDiameter: 200,
                    frontRadius: 200,
                    backRadius: -300,
                    x: -37.5,
                    y: 0
                },
                element2: {
                    depth: 20,
                    frontDiameter: 200,
                    backDiameter: 200,
                    frontRadius: -350,
                    backRadius: 350,
                    x: 10,
                    y: 0
                },
                element3: {
                    depth: 35,
                    frontDiameter: 200,
                    backDiameter: 200,
                    frontRadius: 300,
                    backRadius: Infinity,
                    x: 37.5,
                    y: 0
                }
            }
        };
    },
    components: { Viewport }
}
</script>

<style scoped>

</style>
