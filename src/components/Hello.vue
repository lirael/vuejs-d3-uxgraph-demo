<template>
  <div id="hello">
    </br>
    <h1>{{ msg }}</h1>
    <h2>Graphs list</h2>
    <ul>
      <li><a href="/">Sparklines</a></li>
      <li><a href="/">Line chart</a></li>
      <li><a href="/">Vertical bar chart</a></li>
      <li><a href="/">Horizontal bar chart</a></li>
      <li><a href="/">Staked bar chart</a></li>

    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
    </ul>
    <div class="row">
      <sparklines name="sparklines"></sparklines>
    </div>
    <div class="row">
      <linecharts name="linecharts"></linecharts>
    </div>
    <div class="row">
      <barcharts></barcharts>
    </div>
    <div class="row">
      <horizontal-barcharts></horizontal-barcharts>
    </div>
  </div>
</template>

<script>
import Sparklines from './Sparklines.vue'
import Linecharts from './Linecharts.vue'
import Barcharts from './Barcharts.vue'
import HorizontalBarcharts from './HorBarcharts.vue'
export default {
  name: 'hello',
  components: {
    'sparklines': Sparklines,
    'linecharts': Linecharts,
    'barcharts': Barcharts,
    'horizontal-barcharts': HorizontalBarcharts 
  },
  data () {
    return {
      msg: 'Welcome to the Vue / D3 UX graph construction demo'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
<style type="text/css">
.settings input, settings .button{
}
button{
  background-color: #00897b;
  border: none;
  color: white;
  border-radius: 3px;
}
button.expanded{
  width: 100%;
  margin-top: 1.45em;
}
</style>
