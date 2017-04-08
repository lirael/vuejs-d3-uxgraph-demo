<template>
  <div id="linecharts">
    <h2>{{ msg }}</h2>
    <div class="col-sm-6 col-sm-offset-3" style="">
      <div class="svg-line-container" id="lCanvas">
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
      msg: 'Line charts',
      data: [3, 6, 5, 3, 6, 5, 7, 5, 2, 1, 3, 4, 6, 9, 7, 9]
    }
  },
  mounted () {
    this.createLine('#lCanvas', this.data)
  },
  methods: {
    createLine(id, data) {
      var canvasWidth = 500
      var canvasHeight = 400

      var margins = {top: 0, bottom: 30, left: 25, rigth: 0}

      var width = canvasWidth - margins.left - margins.rigth
      var height = canvasHeight - margins.top - margins.bottom

      var canvas = d3.select(id).append('svg')
        .attr("preserveAspectRatio", "xMinYMin meet")
        .attr("viewBox", "0 0 500 400")
        .classed("svg-content", true)
        .append("svg:g")

      var x = d3.scaleLinear().domain([0, data.length]).range([0, width])
      var y = d3.scaleLinear().domain([0, 10]).range([height, 0])

      // Define the axes
      var xAx = d3.axisBottom(x)
      var yAx = d3.axisLeft(y)

      var line = d3.line()
        .x(function (d, i) {
          return x(i)
        })
        .y(function (d) {
          return y(d)
        })

      canvas
        .append('g')
        .attr('class', 'spark-x axis')
        .attr("transform", "translate(" + margins.left + "," + height + ")")
        .call(xAx)
        .append("text")
        .attr("y", '3em')
        .attr("x", "30em")
        .text("Quantity");
      canvas
        .append('g')
        .attr('class', 'spark-y axis')
        .attr("transform", "translate(" + margins.left + ",0)")
        .call(yAx)
      canvas
        .append('path')
        .attr('class', 'spark')
        .attr("transform", "translate(" + margins.left + ",0)")
        .attr("d", line(data))
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

.svg-line-container {
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
    overflow: visible !important;
    top: 0;
    left: 0;
}

.axis {
    shape-rendering: crispEdges;
}
.spark-x line {
  stroke: lightgrey;
}
.spark-x .minor {
  stroke-opacity: .5;
}
.spark-x path {
  display: block;
}
.spark-y line, .spark-y path {
  fill: #999;
  stroke: #000;
}
.axis path,
.axis line {
    fill: none;
    stroke: grey;
    stroke-width: 1;
    shape-rendering: crispEdges;
}
</style>
