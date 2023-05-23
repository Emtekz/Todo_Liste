<template>
  <!-- Dynamische Klassen (nach :class) -->
  <div class="flex justify-between items-center py-2 px-2" :class="{'bg-green-600': this.todo.done, 'bg-red-600': !this.todo.done}">
    
    <h1 class="cursor-pointer" @click="toggleTodo">
      {{ todo.todo }}
    </h1>

    <button class="bg-black py-1 px-1 rounded" @click="removeTodo">Delete Todo</button>
  </div>
</template>

<script>
export default {
  name: 'TodoList',

  props: ["todoprop", "todoindex"],

  // Variablen 
  // Können mit {{ varName }} ausgegeben werden
  data() {
    return {
      // Bindung an Property
      todo: this.todoprop,
    }
  },

  // Funktionen
  // z.B. mit "v-on:click='Fktn'" aufrufen (= onclick)
  // anstelle von "v-on:" geht auch "@:"
  // methods: {
  //   countUp() {
  //     this.count++;
  //   }
  // }
  methods: {
    toggleTodo() {
      this.$emit("toggledone-index", this.todoindex);
    },

    removeTodo() {
      this.$emit("removetodo-index", this.todoindex);
    }
  },
}
</script>

