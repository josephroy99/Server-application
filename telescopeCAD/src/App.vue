<template>
    <Viewport id="viewport" :elements="elements"/>

    <!--Create a div at the bottom of the screen-->
</template>

<script>
import Viewport from './components/Viewport.vue';

export default {
    name: "App",
    data() {
        return {
            elements: [
                {
                    depth: 75,
                    frontDiameter: 200,
                    backDiameter: 200,
                    frontRadius: 200,
                    backRadius: -300,
                    x: -37.5,
                    y: 0
                },
                {
                    depth: 20,
                    frontDiameter: 200,
                    backDiameter: 200,
                    frontRadius: -350,
                    backRadius: 350,
                    x: 10,
                    y: 0
                },
                {
                    depth: 35,
                    frontDiameter: 200,
                    backDiameter: 200,
                    frontRadius: 300,
                    backRadius: Infinity,
                    x: 37.5,
                    y: 0
                }
            ]
        };
    },
    components: { Viewport }
}
</script>

<style scoped>

</style>
