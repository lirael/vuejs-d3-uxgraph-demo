<template>
  <div id="linecharts">
    <h2>{{ msg }}</h2>
    <div class="col-sm-6 col-sm-offset-3" style="">
      <div class="svg-line-container" id="bCanvas">
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
      msg: 'Vertical bar charts',
      data: [
        { "period": "West", "fail": 23, "success": 57 },
        { "period": "East", "fail": 23, "success": 78 },
        { "period": "North", "fail": 64, "success": 96 },
        { "period": "South", "fail": 21, "success": 54 }
      ]
    }
  },
  mounted () {
    this.createLine('#bCanvas', this.data)
  },
  methods: {
    createLine(id, csv) {
      var canvasWidth = 500
      var canvasHeight = 400
      var margins = {top: 0, bottom: 30, left: 25, rigth: 0}

      var width = canvasWidth - margins.left - margins.rigth
      var height = canvasHeight - margins.top - margins.bottom

      // var width = barHeight * (csv.length - 1)

      var canvas = d3.select(id).append('svg')
        .attr("preserveAspectRatio", "xMinYMin meet")
        .attr("viewBox", "0 0 500 400")
        .classed("svg-content", true)
        .append("svg:g")

      var x = d3.scaleBand()
        .domain(d3.entries(csv).map(function (d) {return d.value.period}))
        .rangeRound([0, width]).padding(0.2)

      var y = d3.scaleLinear()
        // .domain([0, d3.max(csv, function (d) {return d.dollars})])
        .domain([0, 100])
        .range([height, 0])
   
      // Define the axes
      var xAx = d3.axisBottom(x).tickSize(0)
      var yAx = d3.axisLeft(y)

      canvas
        .append('g')
        .attr('class', 'spark-y axis')
        .attr("transform", "translate(" + margins.left + ",0)")
        .call(yAx)

      canvas
        .append('g')
        .attr('class', 'spark-x axis')
        .attr("transform", "translate(" + margins.left + "," + height + ")")
        .call(xAx)

      canvas.selectAll(".success").data(d3.entries(csv))
        .enter()
        .append("rect")
        .attr("transform", "translate(" + margins.left + ",0)")
        .attr('class', 'success')
        .attr("x", function (d) { return x(d.value.period) })
        .attr("width", x.bandwidth()/2)
        .attr("y", function (d) { return y(d.value.success) })
        .attr("height", function (d) { return height - y(d.value.success) })
        .style( "fill", "steelblue" )

      var bar = canvas.selectAll(".fail").data(d3.entries(csv))
        .enter()
        .append("rect")
        .attr("transform", "translate(" + margins.left + ",0)")
        .attr("class", "fail")
        .attr("x", function(d) { return x(d.value.period) + x.bandwidth()/2 })
        .attr("width", x.bandwidth()/2)
        .attr("y", function(d) { return y(d.value.fail); })
        .attr("height", function(d) { return height - y(d.value.fail); })
        .style( "fill", "#d3d3d3" );
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.spark {
  stroke: steelblue;
  stroke-width: 1;
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
