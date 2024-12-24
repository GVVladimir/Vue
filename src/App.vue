<template>
  <div class="div-container">
    <h1 class="div-title">To Do List Vue</h1>
    <ToDoList
      :tasks="tasks"
      @add-task="addTask"
      @remove-task="removeTask"
      @toggle-completion="toggleTask"
    />
  </div>
</template>

<script>
import ToDoList from "./components/ToDoList.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: { ToDoList },
  setup() {
    const tasks = ref([]);

    const addTask = (newTask) => {
      tasks.value.push({
        id: Date.now(),
        text: newTask,
        completed: false,
      });
      const removeTask = (taskId) => {
        tasks.value = tasks.value.filter((task) => task.id !== taskId);
      };

      const toggleTask = (task) => {
        task.completed = !task.completed;
      };
    };

    return { tasks, addTask, toggleTask, removeTask };
  },
};
</script>

<style scoped>
.div-container {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 10px;
  max-width: 600px;
  margin: 40px auto;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.div-title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
}
</style>
