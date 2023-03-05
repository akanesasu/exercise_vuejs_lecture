<template>
  <div class="clearAllContainer">
    <span class="clearAllBtn" v-on:click="clearTodo" style="font-weight: 700"> Clear All </span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo: function () {
      // this.$emit('clearAll')
      this.$store.commit('clearAllItems')
    },
  },
}
</script>

<style scoped>
.clearAllContainer {
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background-color: antiquewhite;
  border-radius: 5px;
  margin: 0 auto;
}
.clearAllBtn {
  color: black;
  display: block;
}
</style>
