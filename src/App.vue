<template>
  <div id="app">
    <todo-card></todo-card>
  </div>
</template>

<script>
import todoCard from './components/todoCard.vue'

export default {
  components: {
    'todo-card': todoCard
  }
}
</script>

<style>

</style>
