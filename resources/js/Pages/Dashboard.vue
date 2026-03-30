<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const tasks = ref([])
const title = ref('')

const fetchTasks = async () => {
    const res = await axios.get('/api/tasks')
    tasks.value = res.data
}

const addTask = async () => {
    if (!title.value) return

    await axios.post('/api/tasks', {
        title: title.value
    })

    title.value = ''
    fetchTasks()
}

const toggleTask = async (task) => {
    await axios.put(`/api/tasks/${task.id}`, {
        is_done: !task.is_done
    })
    fetchTasks()
}

const deleteTask = async (id) => {
    await axios.delete(`/api/tasks/${id}`)
    fetchTasks()
}

onMounted(fetchTasks)
</script>

<template>
<div class="p-6">
    <h1 class="text-xl font-bold mb-4">To-Do List</h1>

    <input v-model="title" placeholder="Add task" class="border p-2 mr-2" />
    <button @click="addTask" class="bg-blue-500 text-white px-3 py-2">Add</button>

    <ul class="mt-4">
        <li v-for="task in tasks" :key="task.id" class="flex items-center gap-2">
            <span 
                :class="{ 'line-through text-gray-400': task.is_done }"
                @click="toggleTask(task)"
                class="cursor-pointer"
            >
                {{ task.title }}
            </span>

            <button @click="deleteTask(task.id)" class="text-red-500">
                X
            </button>
        </li>
    </ul>
</div>
</template>