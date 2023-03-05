<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function () {
    return {
      todoItems: [],
    }
  },
  methods: {
    addOneItem: function (todoItem) {
      const obj = { completed: false, item: todoItem }
      //저장 로직 : 개발자도구 Application
      localStorage.setItem(todoItem, JSON.stringify(obj))
      this.todoItems.push(obj)
    },
    removeOneItem: function (todoItem, index) {
      localStorage.removeItem(todoItem.item)
      this.todoItems.splice(index, 1)
    },
    toggleOneItem: function (todoItem, index) {
      // todoItem.completed = !todoItem.completed
      this.todoItems[index].completed = !this.todoItems[index].completed
      // localStorage는 update가 없어서 지우고 다시 넣어야함
      localStorage.removeItem(todoItem.item)
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
    },
    clearAllItems: function () {
      localStorage.clear()
      this.todoItems = []
    },
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  },
  // TodoList에서 가져옴
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))))
        // this.todoItems.push(localStorage.key(i))
      }
    }
  },
}
</script>

<style>
body {
  display: flex;
  justify-content: center;
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
#app {
  width: 500px;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
