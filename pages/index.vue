<template>
  <div>
    <form>
      <input type="text" v-model="task" placeholder="enter task here">
      <button @click.prevent="save">Save Todo</button>
    </form>

    <h1>List of tasks</h1>
    <ul>
      <li v-for="todo in todos">{{ todo.task }}</li>
    </ul>
  </div>
</template>

<script>
  import Cookies from 'js-cookie'
  export default { 
    data() {
      return {
        task: '',
        todos: []
      }
    },

    mounted() {
      const todosCookie = Cookies.get('todos');
      if(typeof todosCookie !== 'undefined') {
        this.todos = JSON.parse(todosCookie);
      }
    },

    methods: {
      save() {
        this.todos.push({ task: this.task, is_completed: false });
        this.task = '';
        Cookies.set('todos', this.todos);
      }
    }
  }
</script>