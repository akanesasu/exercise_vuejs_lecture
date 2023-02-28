<template>
  <div>
    <app-header v-bind:propsdata="str" v-on:renew="renewStr"></app-header>
    <br/>
    <form v-on:submit.prevent="submitForm">
      <div>
          <label for="username">id : </label>
          <input id="username" type="text" v-model="username">
      </div>
      <div>
          <label for="password">password : </label>
          <input id="password" type="password" v-model="password">
      </div>
      <button type="submit" >login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
export default {
  data: function() {
    return {
      str: 'Test!!!',
      username: '',
      password: '',
    }
  },
  components: {
    'app-header': AppHeader
  },
  methods: {
    renewStr: function() {
      this.str = 'Hi';
    },
    submitForm: function() {
      // event.preventDefault(); : deprecated
      console.log(this.username, this.password);
      const url = 'https://jsonplaceholder.typicode.com/users';
      const data = {
        username: this.username,
        password: this.password
      }
      axios.post(url, data)
        .then(function(response) {
          console.log(response);
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
}
</script>

<style>

</style>