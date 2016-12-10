<template>
  <div class=container id="container">
    <h1 class="text-center">Todo</h1>
    <h4>Todo list: Show {{ showText }}</h4>
    <div class="row">
      <todoDisplay @changeShow="changeShow"></todoDisplay>
      <todo-item 
        v-for="todo in todosToShow" 
        :todoItem="todo"
        @completeTodo="completeTodo"
        @deleteTodo="deleteTodo"
      ></todo-item>
      <br><hr><br>
      <todo-input @newTodo="addTodo"></todo-input>
    </div>
  </div>
</template>

<script>
import uuidV4 from 'uuid/v4';

import todoItem from './components/todoItem.vue';
import todoInput from './components/todoInput.vue';
import todoDisplay from './components/todoDisplay.vue';

export default {
  data () {
    return {
      todos: [
        { id: uuidV4(), text: 'Learn Vuejs', completed: false },
        { id: uuidV4(), text: 'Learn Reactjs', completed: false },
        { id: uuidV4(), text: 'Learn Nodejs', completed: false },
        { id: uuidV4(), text: 'Learn HTML', completed: true },
      ],
      display: 'all'
    }
  },
  computed: {
      todosToShow(){
        switch(this.display){
          case 'all':
            return this.todos;
          case 'completed':
            return this.todos.filter(todo => todo.completed);
          case 'incompleted':
            return this.todos.filter(todo => !todo.completed);
        }
      },
      showText(){
          let text = this.display;
          text = text.charAt(0).toUpperCase() + text.slice(1);

          if(this.display != 'all'){
              text = 'Only ' + text;
          }
          return text;
      }
  },
  components: {
    todoItem,
    todoInput,
    todoDisplay
  },
  methods: {
    deleteTodo(id){
      let targetIdx = this.todos.findIndex(todo => {
        return todo.id == id;
      })
      if(targetIdx != -1) this.todos.splice(targetIdx, 1);
    },
    completeTodo(id){
      let target = this.todos.find(todo => {
        return todo.id == id;
      })
      if(target) target.completed = true;
    },
    addTodo(text){
      const newTodo = {
        id: uuidV4(), 
        text, 
        completed: false
      };
      this.todos.push(newTodo);
    },
    changeShow(newShow){
      this.display = newShow;
    }
  }
}
</script>
<style>
  body {
    padding: 30px;
  }
</style>
