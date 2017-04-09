<template>
  <div id="lines">
    <h1>{{ msg }}</h1>
    <div class="row">
      <div class="col-sm-2 col-sm-offset-3">
        Label: <input v-model="label" :placeholder="label">
      </div>
      <div class="col-sm-2">
        Color: <input v-model="color" :placeholder="color">
      </div>
      <div class="col-sm-2">
        <button class="button expanded" @click="generate()" >
          New random data
        </button>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-6 col-sm-offset-3">
      <br></br>
        <linecharts ref="sparks" 
          :color="color" 
          :label="label">
        </linecharts>
      </div>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'
import Linecharts from './Linecharts.vue'

export default {
  name: 'line-container',
  components: {
    'linecharts': Linecharts
  },
  data () {
    return {
      msg: 'Line charts',
      label: 'Daily defects',
      color: '#4682b4',
      data: [3, 6, 5, 3, 6, 5, 7, 5, 2, 1, 3, 4, 6, 9, 7, 9]
    }
  },
  methods: {
    generate(){
      this.newData()
      var child = this.$refs.sparks
      d3.select('#lCanvas svg').remove()
      child.createLine('#lCanvas', this.data, this.label, this.color)
    },
    newData(){
      this.data = d3.range(10).map(function() {
        var valNew = (Math.round(Math.random() * 10)) + 1
        return valNew
      })
    }
  },
  watch: {
    label: {
      handler: function (val, oldVal) {
        d3.select('#lCanvas svg').remove()
        var child = this.$refs.sparks
        child.createLine('#lCanvas', this.data, val, this.color)
      }
    },
    color: {
      handler: function (val, oldVal) {
        d3.select('#lCanvas svg').remove()
        var child = this.$refs.sparks
        child.createLine('#lCanvas', this.data, this.label, val)
      }
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
