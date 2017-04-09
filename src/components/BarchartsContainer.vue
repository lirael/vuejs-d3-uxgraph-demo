<template>
  <div id="barcharts">
    <h1 style="margin-top:30px;">{{ msg }}</h1>
    <div class="row">
      <div class="col-sm-5 col-sm-offset-2">
        <br></br>
        <barcharts ref="sparks" 
          :colorOne="colorOne" 
          :labelOne="labelOne" 
          :colorTwo="colorTwo" 
          :labelTwo="labelTwo">
        </barcharts>
      </div>
      <div class="col-sm-3">
      <br></br>
        <b> Settings </b>
        <div class="">
        </br>
          Label 1: <input v-model="labelOne" :placeholder="labelOne">
        </div>
        <div class="">
        </br>
          Color 1: <input v-model="colorOne" :placeholder="colorOne">
        </div>
        <div class="">
        </br>
          Label 2: <input v-model="labelTwo" :placeholder="labelTwo">
        </div>
        <div class="">
        </br>
          Color 2: <input v-model="colorTwo" :placeholder="colorTwo">
        </div>
        <div style="">
          <button class="button expanded" style="width:80%; display:none" @click="generate()" >
            New random data
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'
import barcharts from './Barcharts.vue'

export default {
  name: 'barchartsContainer',
  components: {
    'barcharts': barcharts
  },
  data () {
    return {
      msg: 'Vertical bar charts',
      labelOne: 'Success',
      colorOne: '#4682B4',
      labelTwo: 'Fail',
      colorTwo: '#d3d3d3',
      data: [
        { "period": "West", "fail": 23, "success": 57 },
        { "period": "East", "fail": 23, "success": 78 },
        { "period": "North", "fail": 64, "success": 96 },
        { "period": "South", "fail": 21, "success": 54 }
      ]
    }
  },
  methods: {
    generate(){
      this.newData()
      var child = this.$refs.sparks
      d3.select('#bCanvas svg').remove()
      child.createLine('#bCanvas', this.data, this.label, this.circle, this.color)
    },
    newData(){
      this.data = d3.range(10).map(function() {
        var valNew = (Math.round(Math.random() * 10)) + 1
        return valNew
      })
    }
  },
  watch: {
    labelOne: {
      handler: function (val, oldVal) {
        d3.select('#bCanvas svg').remove()
        var child = this.$refs.sparks
        child.createLine('#bCanvas', this.data, val, this.colorOne, this.labelTwo, this.colorTwo)
      }
    },
    colorOne: {
      handler: function (val, oldVal) {
        d3.select('#bCanvas svg').remove()
        var child = this.$refs.sparks
        child.createLine('#bCanvas', this.data, this.labelOne, val, this.labelTwo, this.colorTwo)
      }
    },
    labelTwo: {
      handler: function (val, oldVal) {
        d3.select('#bCanvas svg').remove()
        var child = this.$refs.sparks
        child.createLine('#bCanvas', this.data, this.labelOne, this.colorOne, val, this.colorTwo)
      }
    },
    colorTwo: {
      handler: function (val, oldVal) {
        d3.select('#bCanvas svg').remove()
        var child = this.$refs.sparks
        child.createLine('#bCanvas', this.data, this.labelOne, this.colorOne, this.labelTwo, val)
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
