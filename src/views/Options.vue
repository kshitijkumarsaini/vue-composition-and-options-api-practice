<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>You have {{ numTodos }} Todo's!</h3>
    <div>
      <input
        v-model="newTodoName"
        @keyup.enter="addTodo"
        type="text"
        placeholder="Add a todo"
      >
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="removeTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      newTodoName: '',
      todos: [],
      negativeWords: ['fuck', 'kiss', 'nude', 'sex', 'fart', 'lick', 'bitch', 'dick', 'vagina', 'pussy', 'butt', 'ass']
    }
  },
  computed: {
    numTodos() {
      return this.todos.length;
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: Date.now(),
        name: this.newTodoName
      });
      this.newTodoName = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    }
  },
  watch: {
    newTodoName(newVal) {
      if(this.negativeWords.includes(newVal.toLowerCase())) {
        this.newTodoName = '';
        alert('Bad words are prohibited!');
      }
    }
  }
}
</script>

<style>
 ul {
   list-style: none;
   padding: 0;
   width: 200px;
   margin: 20px auto 0;
 }
 li {
   border: 1px solid;
   display: flex;
   margin-bottom: 10px;
 }
 li span {
   flex-grow: 1;
 }
</style>