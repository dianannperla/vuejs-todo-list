<template>
  <div id="app">
    <h1>Danh Sách Việc Cần Làm</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Thêm việc mới..." />
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.name }}</span>
        <button @click="removeTask(index)">Xóa</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: JSON.parse(localStorage.getItem('tasks')) || []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ name: this.newTask, completed: false });
        this.newTask = '';
        this.saveTasks();
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
  }
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
#app {
  max-width: 600px;
  margin: auto;
}
input {
  margin-right: 10px;
}
</style>
