<script setup lang="ts">
import { defineProps, withDefaults } from "vue";

interface Props {
  todo: {
    id: number;
    text: string;
    completed: boolean;
  };
}

const props = withDefaults(defineProps<Props>(), {
  todo: () => ({
    id: 0,
    text: "",
    completed: false,
  }),
});

const emit = defineEmits(["toggle-complete", "delete-todo"]);

const toggleComplete = () => {
  emit("toggle-complete", props.todo.id);
};

const deleteTodo = () => {
  emit("delete-todo", props.todo.id);
};
</script>

<template>
  <li class="flex items-center justify-between py-2 border-b border-gray-200">
    <input
      type="checkbox"
      :checked="props.todo.completed"
      @change="toggleComplete"
      class="mr-2"
    />
    <span :class="{ 'line-through': props.todo.completed }">
      {{ props.todo.text }}
    </span>
    <button @click="deleteTodo" class="text-red-500 hover:text-red-700">
      Delete
    </button>
  </li>
</template>
