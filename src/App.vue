<template>
  <div id="app">
    <Header></Header>
    <Input v-on:addTodo="addTodo"></Input>
    <List v-bind:propsdata="todoItems" @removeTodo="removeTodo"></List>
    <Footer v-on:removeAll="clearAll"></Footer>
  </div>
</template>

<script>
import Header from './components/Header'
import Input from './components/Input'
import List from './components/List'
import Footer from './components/Footer'

export default {
  name: 'App',
  data() { return { todoItems: [] } },
  created() {
    if (localStorage.length > 0) {
      for (var i=0; i<localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    addTodo(todoItem) {
    localStorage.setItem(todoItem, todoItem);
    this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
			localStorage.removeItem(todoItem);
			this.todoItems.splice(index, 1);
		}
  },
  components: { Header, Input, List, Footer }
}
</script>

<style>
  body { text-align: center; background-color: #f6f6f8;}
  #app {  margin: auto; width: 400px; }
  input { border-style:  groove; width: 200px; text-align: center;}
  button { border-style: groove; }
  .shadow { box-shadow: 5px 10px 10px rgba(0,0,0,0.03); }
</style>