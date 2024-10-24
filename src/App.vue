<script setup>
import { ref, onMounted } from 'vue'
const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['Task One', 'Task Two', 'Task Three', 'Task Four']);
const link = ref('https://google.com');
const newTask = ref('')

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/todos');
    console.log(res)
    const data = await res.json()
    console.log(data)
    tasks.value = data.map(task => task.title)
  } catch (error) {
    console.error(error)
  }
})
</script>

<template>
  <h1 class="text-slate-400" v-if="status == 'active'" v-text="name"></h1>
  <h2 class="text-red-400" v-else>{{ name }}</h2>
  <div>
    <li v-for="(task, index) in tasks" :key="index"> <span>{{ task }}</span> <button
        @click="deleteTask(index)">Delete</button>
    </li>
  </div>

  <button @click="toggleStatus">Toggle status</button>

  <form @submit.prevent="addTask">
    <label for="newTask" class="block text-xl my-3">Add New Task:</label>
    <input type="text" id="newTask" v-model="newTask" class="border border-gray-300 rounded-md px-3 py-2 w-full" />
    <button type="submit" class="mt-3 px-4 py-2 bg-green-500 text-white rounded-md">
      Add Task
    </button>
  </form>
</template>

<style scoped></style>
