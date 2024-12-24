<template>
  <li :class="{ completed: task.completed }" class="todo-item">
    <span @click="$emit('toggle-completion', task)" class="task-text">
        {{ task.text }}
    </span>
    <button @click="$emit('remove-task', task.id)" class="remove-button">Удалить</button>
  </li>
</template>

<script>
import { ref } from "vue";
import ToDoList from './ToDoList.vue'

export default {
  name: "ToDoItem",
  props: ["task"],
  emits: ["toggle-completion", "remove-task"],
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.completed .task-text {
  text-decoration: line-through;
  color: #aaa;
}
</style>
