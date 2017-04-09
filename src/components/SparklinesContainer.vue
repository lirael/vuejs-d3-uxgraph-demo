<template>
  <div id="sparklines">
    <h1>{{ msg }}</h1>
    <div class="row">
      <div class="col-sm-2 col-sm-offset-2">
        Label: <input v-model="label" :placeholder="label">
      </div>
      <div class="col-sm-2">
        Color: <input v-model="color" :placeholder="color">
      </div>
      <div class="col-sm-2">
        <button v-if="circle" class="button expanded" @click="circle = false">
          Hide red dot
        </button>
        <button v-if="!circle" class="button expanded" @click="circle = true">
          Show red dot
        </button>
      </div>
      <div class="col-sm-2">
        <button class="button expanded" @click="generate()" >
          New random data
        </button>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-4 col-sm-offset-4"  style="height:150px">
      <br></br>
        <sparklines ref="sparks" 
          :color="color" 
          :label="label" 
          :circle="circle">
        </sparklines>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-4 col-sm-offset-4">
      Embed following code to get this sparkline:
      <textarea class="html-viewer" disabled rows="4"><sparklines color="{{color}}" 
  label="{{label}}" 
  circle="{{circle}}">
</sparklines> </textarea>
      </div>
    </div>
  </div>
</template>

<script>
import Sparklines from './Sparklines.vue'
import * as d3 from 'd3'

export default {
  name: 'SparklinesContainer',
  components: {
    'sparklines': Sparklines
  },
  data () {
    return {
      msg: 'Sparklines',
      label: 'Daily defects',
      color: '#4682b4',
      circle: false,
      data: [0, 2, 3, 5, 4, 10, 4, 11, 10, 15, 4, 11, 10, 9, 5, 11, 15, 9, 10, 11, 15]
    }
  },
  methods: {
    generate(){
      this.newData()
      var child = this.$refs.sparks
      d3.select('#sCanvas svg').remove()
      child.createSparkline('#sCanvas', this.data, this.label, this.circle, this.color)
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
        d3.select('#sCanvas svg').remove()
        var child = this.$refs.sparks
        child.createSparkline('#sCanvas', this.data, val, this.circle, this.color)
      }
    },
    color: {
      handler: function (val, oldVal) {
        d3.select('#sCanvas svg').remove()
        var child = this.$refs.sparks
        child.createSparkline('#sCanvas', this.data, this.label, this.circle, val)
      }
    },
    circle: {
      handler: function (val, oldVal) {
        d3.select('#sCanvas svg').remove()
        var child = this.$refs.sparks
        child.createSparkline('#sCanvas', this.data, this.label, val, this.color)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.spark-path {
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
