<script setup lang="ts">
import { ref } from "vue";
import TodoItem from "./components/TodoItem.vue";

const newTodoText = ref("");
const todos = ref([
  { id: 1, text: "Learn Vue", completed: false },
  { id: 2, text: "Build a To-Do App", completed: true },
]);

let nextTodoId = 3;

const addTodo = () => {
  if (newTodoText.value.trim() !== "") {
    todos.value.push({
      id: nextTodoId++,
      text: newTodoText.value,
      completed: false,
    });
    newTodoText.value = "";
  }
};

const toggleComplete = (id: number) => {
  const todo = todos.value.find((todo) => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

const deleteTodo = (id: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <div class="container mx-auto p-4">
    <header class="mb-6 shadow-lg rounded-md p-4">
      <h1 class="text-3xl font-bold">SPA Webie: To-Do📒List</h1>
    </header>

    <main>
      <div class="flex mb-4">
        <input
          type="text"
          v-model="newTodoText"
          placeholder="Add a new to-do note item."
          class="flex-grow border border-gray-300 px-4 py-2 rounded-l-md focus:outline-none focus:ring focus:ring-blue-500"
        />
        <button
          @click="addTodo"
          class="bg-blue-500 text-white px-4 py-2 rounded-r-md hover:bg-blue-600 focus:outline-none focus:ring focus:ring-blue-500"
        >
          Add
        </button>
      </div>

      <ul>
        <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @toggle-complete="toggleComplete"
          @delete-todo="deleteTodo"
        />
      </ul>
    </main>

    <footer class="text-center py-4 mt-6 flex flex-col">
      <a
        href="mailto:jozef.javorsky.dodo@gmail.com"
        class="text-blue-500 hover:text-blue-700 font-medium"
      >
        jozef.javorsky.dodo@gmail.com
      </a>
      <a
        href="https://github.com/jozef-javorsky-dodo"
        target="_blank"
        rel="noopener noreferrer"
        class="text-blue-500 hover:text-blue-700 font-medium"
      >
        GitHub-profile
      </a>
    </footer>
  </div>
</template>
