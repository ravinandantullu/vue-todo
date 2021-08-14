<template>
  <h1>Todo Application</h1>
  <form @submit.prevent="addNewTodo()">
    <label for="enterTodo">New Todo</label>
    <input v-model="newTodo" type="text" name="enterTodo" />
    <button>Add todo</button>
  </form>
  <button @click="markAllDone()">Mark All Done</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id">
      <h1 :class="{ done: todo.done }" @click="toggleDone(todo)" class="todo">
        {{ todo.content }}
      </h1>
      <button @click="removeTodo(index)">Remove todo</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Todo",
  props: {},

  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: new Date(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
      console.log(todo);
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
      console.log(index);
    }

    function markAllDone() {
      todos.value.map((value) => {
        value.done = true;
      });
    }

    return {
      newTodo,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
    };
  },
};
</script>

<style scoped>
h1 {
  color: aqua;
}

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>