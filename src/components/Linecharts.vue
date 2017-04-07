<template>
  <div id="linecharts">
    <h2>{{ msg }}</h2>
    <div class="col-sm-6 col-sm-offset-3" id="lCanvas" style="height:150px"></div>
  </div>
</template>

<script>
import * as d3 from 'd3'
import $ from 'jquery'

export default {
  name: 'sparklines',
  data () {
    return {
      msg: 'Line charts',
      data: [3, 6, 2, 7, 5, 2, 1, 3, 8, 9, 2, 5, 9, 3, 6, 3, 6, 2, 7, 5, 2, 1, 3, 8, 9, 2, 5, 9, 2, 7, 5, 2, 1, 3, 8, 9, 2, 5, 9, 3, 6, 2, 7, 5, 2, 1, 3, 8, 9, 2, 9]
    }
  },
  mounted () {
    this.createSparkline('#lCanvas', this.data)
  },
  methods: {
    createSparkline(id, data) {
      var width = 500
      var height = 65
      var canvas = d3.select(id).append('svg').attr('width', '100%').attr('height', '100%')
      var x = d3.scaleLinear().domain([0, 48]).range([0, width])
      var y = d3.scaleLinear().domain([0, 10]).range([height, 0])
      var line = d3.line()
        .x(function (d, i) {
          return x(i)
        })
        .y(function (d) {
          return y(d)
        })
        .curve(d3.curveBasis)

      canvas
        .append('path')
        .attr('class', 'spark')
        .attr('d', line(data))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.spark {
  stroke: steelblue;
  stroke-width: 1;
  fill: none;
}

</style>
