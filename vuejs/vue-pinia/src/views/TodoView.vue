<template>
  <div class="todo-list">
    <h1>To-Do List</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id" :class="{ completed: task.completed }">
        <span>{{ task.title }}</span>
        <button @click="toggleTaskCompleted(task.id)">
          {{ task.completed ? "Belum Selesai" : "Selesai" }}
        </button>
        <button @click="deleteTask(task.id)">Hapus</button>
      </li>
    </ul>
    <div class="add-task">
      <input type="text" v-model="newTaskTitle" placeholder="Tugas Baru" />
      <button @click="addTask">Tambah</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { id: 1, title: "Belajar Vue.js", completed: false },
        { id: 2, title: "Kerjakan PR", completed: true },
      ],
      newTaskTitle: "",
    };
  },
  methods: {
    addTask() {
      if (this.newTaskTitle) {
        this.tasks.push({
          id: Date.now(),
          title: this.newTaskTitle,
          completed: false,
        });
        this.newTaskTitle = "";
      }
    },
    toggleTaskCompleted(taskId) {
      const task = this.tasks.find((task) => task.id === taskId);
      task.completed = !task.completed;
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId);
    },
  },
};
</script>

<style scoped>
.todo-list {
  max-width: 400px;
  margin: 0 auto;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.completed {
  text-decoration: line-through;
}

.add-task {
  margin-top: 20px;
}

input[type="text"] {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 8px 12px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
