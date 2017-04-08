<template>
  <div id="sparklines">
    <h2>{{ msg }}</h2>
    <div class="col-sm-4 col-sm-offset-4"  style="height:150px">
    </br>
      <div class="svg-container" id="sCanvas">
      </div>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'
import $ from 'jquery'

export default {
  name: 'sparklines',
  data () {
    return {
      msg: 'Sparklines',
      data: [0, 2, 3, 5, 4, 10, 4, 11, 10, 15, 4, 11, 10, 9, 5, 11, 15, 9, 10, 11, 15]
    }
  },
  mounted () {
    this.createSparkline('#sCanvas', this.data)
  },
  methods: {
    createSparkline(id, data) {
      var canvasWidth = $('#sCanvas').parent().width()
      var canvasHeight = 40

      var margins = {top: -4, bottom: 0, left: 0, rigth: 4}

      var width = canvasWidth - margins.left - margins.rigth
      var height = canvasHeight - margins.top - margins.bottom

      var canvas = d3.select(id).append('svg')
        .attr("preserveAspectRatio", "xMinYMin meet")
        .attr("viewBox", "viewBox", "0 0 "+ width +" " + height +"")
        .classed("svg-content", true)

      var x = d3.scaleLinear().domain([0, data.length]).range([0, width])
      var y = d3.scaleLinear().domain([0, d3.max(data)]).range([height, 0])

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
        .attr("transform", "translate(" + margins.right + ", " + margins.top + ")")
        .attr('d', line(data))

      canvas
        .append('circle')
        .attr('class', 'sparkcircle')
        .attr('cx', x(data.length - 1))
        .attr('cy', y(d3.max(data)))
        .attr('r', 2)
        .attr('fill', 'red')
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
.svg-container {
    display: inline-block;
    position: relative;
    width: 100%;
    padding-bottom: 100%;
    vertical-align: top;
    overflow: visible;
}
.svg-content {
    display: inline-block;
    position: absolute;
    top: 0;
    left: 0;
}

#sCanvas{
  display: inline-block;
}

</style>
