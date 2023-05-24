<template>
  <div class="bg-gray-600 text-white w-2/3 m-auto mt-12">
    <div class="text-center border-b-2 border-black py-4">
      <h1 class="text-3xl py-4">Unsere Todos</h1>
      <p class="text-xl" v-if="opentodos.length > 0">Offene To-Do's: {{ opentodos.length }}/{{ todos.length }}</p>
      <p class="text-xl" v-else>Keine Offenen To-Do's</p>

      <div class="mt-4 px-2">
        <form action="#" @submit.prevent="addTodo">
          <input
          type="text"
          class="py-2 px-2 w-2/3 text-black"
          v-model="newTodo"
          />
          <button class="bg-red-400 py-2 w-1/3" @click="addTodo">
            Add To-Do
          </button>
        </form>
      </div>
    </div>

    <div v-for="(todo, index) in todos" :key="todo.todo">
      <!-- Übergabe von Werten aus todos Array -->
      <TodoList
        :todoprop="todo"
        :todoindex="index"
        @toggledone-index="toggleDone"
        @removetodo-index="deleteTodo"
      />
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",

  data() {
    return {
      newTodo: "",
      todos: [],
    }
  },

  mounted() {
    let data = localStorage.getItem("todos");

    if(data !== "" && data !== null){

      this.todos = JSON.parse(data);
    }
    else {
      this.todos = [];
    }

  },

  computed: {
    opentodos() {
      const openTodos = this.todos.filter((todo) => {
        return !todo.done
      })

      return openTodos;
    }
  },

  components: {
    TodoList,
  },

  methods: {
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;

      this.storeTodos();
    },

    deleteTodo(index) {
      this.todos.splice(index, 1);

      this.storeTodos();
    },

    addTodo() {
      if(this.newTodo.trim() === "") {
        return;
      }
      else {
        this.todos.push({todo: this.newTodo, done: false});
        this.newTodo = "";

        this.storeTodos();
      }
    },

    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>
