<template>
  <AddTask v-if="showTask" @add-task="addTask" />
  <Tasks
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";
import axios from "axios";

const baseUrl = "http://localhost:3000/tasks"

export default {
  name: "Home",
  props: {
      showTask: Boolean
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      if (confirm("Are you Sure?")) {
        const response = await axios.delete(`${baseUrl}/${id}`);
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    async toggleReminder(id) {
      const toggleTask = await this.fetchTask(id);
      const updToggle = { ...toggleTask, reminder: !toggleTask.reminder };
      const response = await axios.put(`${baseUrl}/${id}`, updToggle)
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: response.data.reminder } : task
      );
    },
    async addTask(task) {
      const response = await axios.post(baseUrl, task);
      this.tasks = [...this.tasks, response.data];
    },
    async fetchTasks() {
      const response = await axios.get(baseUrl);
      this.tasks = response.data
      return response.data;
    },
    async fetchTask(id) {
      const response = await axios.get(`${baseUrl}/${id}`);
      return response.data;
    },
  },
  created() {
    this.fetchTasks();
  },
};
</script>
