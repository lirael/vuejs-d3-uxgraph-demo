<template>
  <div id="hello">
    </br>
    <h1>{{ msg }}</h1>
    <h2>Graphs list</h2>
    <ul>
      <li><a href="#sparklines">Sparklines</a></li>
      <li><a href="#linecharts">Line chart</a></li>
      <li><a href="#barcharts">Bar chart</a></li>
      <li><a href="#bulletcharts">Bullet chart</a></li>
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
  </div>
</template>

<script>
import Sparklines from './Sparklines.vue'
import Linecharts from './Linecharts.vue'
export default {
  name: 'hello',
  components: {
    'sparklines': Sparklines,
    'linecharts': Linecharts
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
