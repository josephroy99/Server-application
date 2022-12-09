<template>
<!--create svg 100 wide and 100 high-->
  <svg :height="viewHeight" :width="viewWidth">
    <polygon @click="test()" v-bind:points="ComplilePointsString(75,200,200,200,-300,0,0)" style="fill:aqua;stroke:purple;stroke-width:0.3"/>
    <polygon @click="test()" v-bind:points="ComplilePointsString(20,200,200,-350,350,47.5,0)" style="fill:aqua;stroke:purple;stroke-width:0.3"/>
    <polygon @click="test()" v-bind:points="ComplilePointsString(35,200,200,300,Infinity,75,0)" style="fill:aqua;stroke:purple;stroke-width:0.3"/>
  </svg>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      viewWidth: 400,
      viewHeight: 400
    }
  },
  methods: {
    test: function() {
      console.log("test");
    },
    CreatePolygon: function(depth, diameter, radius, xPos, yPos) {
      var points = [];
      let iterations = 51.0;

      if (radius === Infinity) {
        for (let i = 1; i >= -1; i -= 2) {
          let xBack = this.viewWidth / 2.0 + xPos + depth / 2.0;
          let yBack = this.viewHeight / 2.0 + yPos + diameter * i / 2.0;
          let xFront = this.viewWidth / 2.0 + xPos - depth / 2.0;
          let yFront = this.viewHeight / 2.0 + yPos - diameter * i / 2.0;

          points.push({front:{x:xFront, y:yFront}, back:{x:xBack, y:yBack}});
          console.log("Surface is flat");
        }

        return points;
      }

      if (Math.abs(radius) < diameter / 2.0) {
        console.log("Radius is too small");
        radius = diameter / 2.0 * Math.sign(radius);
        console.log("Radius is now " + radius);
      }
      
      let limit = Math.asin(diameter / 2.0 / radius);

      for (let i = 0; i <= iterations; i++) {
        let h = i / iterations;
        let u = (Math.PI / 2.0 - limit) + (2.0 * limit * h);

        let x = radius * Math.sin(u + Math.PI) + radius + xPos;

        let xBack = x + depth / 2.0 + this.viewWidth / 2.0;
        let yBack = radius * Math.cos(u) + yPos + this.viewHeight / 2.0;
        let xFront = x - depth / 2.0 + this.viewWidth / 2.0;
        let yFront = radius * Math.cos(u + Math.PI) + yPos + this.viewHeight / 2.0;
        
        points.push({front:{x:xFront, y:yFront}, back:{x:xBack, y:yBack}});
      }

      return points;
    },
    ComplilePointsString: function(depth, frontDiameter, backDiameter, frontRadius, backRadius, x, y) {
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

  }
}
</script>

<style scoped>

</style>
