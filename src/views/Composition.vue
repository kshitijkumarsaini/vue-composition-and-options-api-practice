<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h3>You have {{ numTodos }} Todo's!</h3>
    <div>
      <input
        v-model="data.newTodoName"
        @keyup.enter="addTodo"
        type="text"
        placeholder="Add a todo"
      />
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in data.todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="removeTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed, watch } from "vue";

export default {
  setup() {
    // Variables
    /**
     * 
      let newTodoName = ref('');
      const todos = ref([]);
    */
    const negativeWords = [
      "fuck",
      "kiss",
      "nude",
      "sex",
      "fart",
      "lick",
      "bitch",
      "dick",
      "vagina",
      "pussy",
      "butt",
      "ass",
    ];

    // Reactive
    let data = reactive({
      newTodoName: "",
      todos: [],
    });

    // Computed
    let numTodos = computed(() => {
      // return todos.value.length;
      return data.todos.length;
    });

    // Methods
    // function addTodo() {
    //   todos.value.push({
    //     id: Date.now(),
    // name: newTodoName.value
    // });
    // newTodoName.value = '';
    // };
    function addTodo() {
      data.todos.push({
        id: Date.now(),
        name: data.newTodoName,
      });
      data.newTodoName = "";
    }

    function removeTodo(index) {
      // todos.value.splice(index, 1);
      data.todos.splice(index, 1);
    }

    // Watchers
    // watch(newTodoName.value, (newVal) => {
    //   if (negativeWords.includes(newVal.toLowerCase())) {
    //     // newTodoName.value = '';
    //     alert("Bad words are prohibited!");
    //   }
    // });

    watch(data, (newVal) => {
      if(negativeWords.includes(newVal.newTodoName.toLowerCase())) {
        data.newTodoName = "",
        alert('Bad words are prohibited!');
      }
    })

    return {
      // newTodoName,
      // todos,
      data,

      numTodos,

      addTodo,
      removeTodo,
    };
  },
  // data() {
  //   return {
  //     newTodoName: '',
  //     todos: [],
  //     negativeWords: ['fuck', 'kiss', 'nude', 'sex', 'fart', 'lick', 'dick', 'vagina', 'pussy', 'butt', 'ass']
  //   }
  // },
  // computed: {
  //   numTodos() {
  //     return this.todos.length;
  //   }
  // },
  // methods: {
  //   addTodo() {
  //     this.todos.push({
  //       id: Date.now(),
  //       name: this.newTodoName
  //     });
  //     this.newTodoName = '';
  //   },
  //   removeTodo(index) {
  //     this.todos.splice(index, 1);
  //   }
  // },
  // watch: {
  //   newTodoName(newVal) {
  //     if(this.negativeWords.includes(newVal.toLowerCase())) {
  //       this.newTodoName = '';
  //       alert('Bad words are prohibited!');
  //     }
  //   }
  // }
};
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