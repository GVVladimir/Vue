<template>
  <div class="todo_list">
    <form @submit.prevent="addTaskNew" class="todo-form">
      <input
        v-model="inputNewTask"
        placeholder="Введите новую задачу"
        class="todo-input"
      />
      <button type="submit" class="todo-button">Добавить</button>
    </form>
    <ul class="todo-list">
      <ToDoItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @remove-task="$emit('remove-task', $event)"
        @toggle-completion="$emit('toggle-completion', $event)"
      />
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
import ToDoItem from "./ToDoItem.vue";

export default {
  name: "ToDoList",
  props: ["tasks"],
  emits: ["add-task", "toggle-completion", "remove-task"],
  components: { ToDoItem },
  setup(_, { emit }) {
    const inputNewTask = ref("");
    const addTaskNew = () => {
      if (inputNewTask.value.trim() !== "") {
        emit("add-task", inputNewTask.value);
        inputNewTask.value = "";
      }
    };
    return { inputNewTask, addTaskNew };
  },
};
</script>

<style scoped>
.todo_list {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.todo-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.todo-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.todo-button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.todo-button:hover {
  background-color: #45a049;
}

.todo-list {
  list-style: none;
  padding: 0;
}
</style>
