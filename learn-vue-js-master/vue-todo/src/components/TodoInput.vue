<template>
  <div>
    <input type="text" v-model="newTodoItem" />
    <button v-on:click="addTodo">add</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTodoItem: '',
    }
  },
  methods: {
    addTodo: function () {
      //저장 로직 : 개발자도구 Application
      localStorage.setItem(this.newTodoItem, this.newTodoItem)
      this.newTodoItem = ''
    },
  },
}
</script>

<style></style>
