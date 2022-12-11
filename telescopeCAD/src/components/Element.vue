<template>
    <polygon class="element" :points="ComplilePointsString(ElementProperties.depth, ElementProperties.frontDiameter, ElementProperties.backDiameter, ElementProperties.frontRadius, ElementProperties.backRadius, ElementProperties.x, ElementProperties.y)"/>
</template>

<script>
    export default {
        name: Element,
        data() {
            return {
                viewWidth: 100,
                viewHeight: 100
            }
        },
        props: {
            ElementProperties: {
                type: Object
            }
        },
        methods: {
            CreatePolygon: function (depth, diameter, radius, xPos, yPos) {
                var points = [];
                let iterations = 51;

                if (radius === Infinity) {
                    for (let i = 1; i >= -1; i -= 2) {
                        let xBack = this.viewWidth / 2 + xPos + depth / 2;
                        let yBack = this.viewHeight / 2 + yPos + diameter * i / 2;
                        let xFront = this.viewWidth / 2 + xPos - depth / 2;
                        let yFront = this.viewHeight / 2 + yPos - diameter * i / 2;
                        points.push({ front: { x: xFront, y: yFront }, back: { x: xBack, y: yBack } });
                    }
                    return points;
                }

                if (Math.abs(radius) < diameter / 2) {
                    console.log("Radius is too small");
                    radius = diameter / 2 * Math.sign(radius);
                    console.log("Radius is now " + radius);
                }

                let limit = Math.asin(diameter / 2 / radius);
                for (let i = 0; i <= iterations; i++) {
                    let h = i / iterations;
                    let u = (Math.PI / 2 - limit) + (2 * limit * h);
                    let x = radius * Math.sin(u + Math.PI) + radius + xPos;
                    let xBack = x + depth / 2 + this.viewWidth / 2;
                    let yBack = radius * Math.cos(u) + yPos + this.viewHeight / 2;
                    let xFront = x - depth / 2 + this.viewWidth / 2;
                    let yFront = radius * Math.cos(u + Math.PI) + yPos + this.viewHeight / 2;
                    points.push({ front: { x: xFront, y: yFront }, back: { x: xBack, y: yBack } });
                }

                return points;
            },
            ComplilePointsString: function (depth, frontDiameter, backDiameter, frontRadius, backRadius, x, y) {
                let pointsFront = this.CreatePolygon(depth, frontDiameter, frontRadius, x, y);
                let pointsBack = this.CreatePolygon(depth, backDiameter, backRadius, x, y);
                let pointsString = "";

                for (let i = 0; i < pointsFront.length; i++) {
                    pointsString += pointsFront[i].front.x + "," + pointsFront[i].front.y + "\n";
                }
                for (let i = 0; i < pointsBack.length; i++) {
                    pointsString += pointsBack[i].back.x + "," + pointsBack[i].back.y + "\n";
                }

                return pointsString;
            }
        },
        mounted: function () {
            this.viewWidth = document.getElementById("viewport").clientWidth;
            this.viewHeight = document.getElementById("viewport").clientHeight;
        }
    }
</script>

<style>
    .element {
        fill: aqua;
        stroke: purple;
        stroke-width: 0.3;
    }
</style>