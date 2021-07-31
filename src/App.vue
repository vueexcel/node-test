<template>
  <div id="app">
    <Node />
  </div>
</template>

<script>
import Node from './components/Node.vue'

export default {
  name: 'App',
  components: {
    Node
  }
}
</script>

<style>
#app {
 display: flex;
 margin-top: 10px ;
}
</style>
