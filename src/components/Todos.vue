<template lang="html">
<section class="todoapp">
  <header class="header">
    <h1>TodoList</h1>
    <input type="text" class="new-todo" placeholder="ajouter une tache" v-model="newTodo" v-on:keyup.enter="addTodo">
  </header>
  <div class="main">
  <input id="toggle-all" type="checkbox" class="toggle-all" v-model="allDone">
  <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <li class="todo" v-for="todo in filteredTodos" v-bind:class="{completed: todo.completed,editing: todo === editing}">
        <div class="view">
          <input type="checkbox" class="toggle" v-model="todo.completed">
          <label v-on:dblclick="editTodo(todo)">{{todo.name}}</label>
          <button type="button" class="destroy" v-on:click="deleteTodo(todo)"></button>
        </div>
        <input type="text" class="edit" v-model="todo.name" v-on:keyup.enter="doneEdit" v-on:keyup.esc="cancelEdit" v-on:blur="doneEdit" v-focus="todo == editing">
      </li>
    </ul>
  </div>
  <footer class="footer" v-show="hasTodos">
    <span class="todo-count"><strong>{{remaining}}</strong>Taches a faire</span>
    <ul class="filters">
      <li><a href="#" v-bind:class="{selected:filter =='all'}" v-on:click.prevent="filter='all'">Toutes</a></li>
      <li><a href="#" v-bind:class="{selected:filter =='todo'}" v-on:click.prevent="filter='todo'">A faire</a></li>
      <li><a href="#" v-bind:class="{selected:filter =='done'}" v-on:click.prevent="filter='done'">Faites</a></li>
    </ul>
    <button type="button"class="clear-completed" v-on:click.prevent="deleteCompleted" v-show="completed">Clear completed</button>
  </footer>
</section>
</template>

<script>
export default {
  name:'todos',
  data(){
    return {
      newTodo:'',
      todos:[],
      filter:'all',
      editing:null,
      oldTodo:''
    }
  },
  methods:{
    addTodo(){
      this.todos.push({
        completed:false,
        name:this.newTodo
      })
      this.newTodo = ''
    },
    deleteTodo(todo){
      this.todos = this.todos.filter(i => i !== todo )
    },
    completed(){
      return this.todos.filter(todo => todo.completed).length
    },
    deleteCompleted(todo){
      this.todos = this.todos.filter(todo => !todo.completed )
    },
    editTodo(todo){
      this.editing = todo;
      this.oldTodo = todo.name;
    },
    doneEdit(){
      this.editing = null
    },
    cancelEdit(){
      this.editing.name = this.oldTodo;
      this.doneEdit()
    }
  },
  computed: {
    allDone:{
      get(){
        return this.remaining === 0
      },
      set(value){
        if(value == true){
          this.todos.forEach(todo => {
            todo.completed = value;
          })
        }else {
          this.todos.forEach(todo => {
            todo.completed = value;
          })
        }
      }
    },
    remaining(){
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos(){
      if (this.filter =='todo') {
        return this.todos.filter(todo => !todo.completed)
      }else if(this.filter =='done'){
        return this.todos.filter(todo => todo.completed)
      }else{
        return this.todos
      }
    },
    hasTodos(){
      return this.todos.length > 0
    },
  },
  directives:{
    focus(el,value){
      if (value) {
        el.focus()
      }
    }
  }
}
</script>

<style scoped>

</style>
