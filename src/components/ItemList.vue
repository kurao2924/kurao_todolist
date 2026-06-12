<!-- src/components/ItemList.vue -->
<script setup lang="ts">
import { ref } from 'vue'

interface Task{
    name:string,
    done:boolean
}

const not_done_tasks = ref<Task[]>([ 
  { name: 'たまご', done: false }, 
  { name: 'りんご', done: false }
])

const completed_tasks=ref<Task[]>([ ])
let newTaskName = ref('')  

const addTask = () => { 
    if (newTaskName.value==''){
        return
    }
  not_done_tasks.value.push({ name: newTaskName.value, done:false}) 
  newTaskName = ref('') 
} 

const completeTask = (task: Task) => { 
  not_done_tasks.value.splice(not_done_tasks.value.indexOf(task),1)
  completed_tasks.value.push(task)
} 
</script>

<template>
    <div>
    <div>未完了</div>
      <ul>
      <li v-for="task in not_done_tasks" :key="task.name">
        <div>タスク名: {{ task.name }}</div>
        <button @click="completeTask(task)">完了</button>
      </li>
    </ul>
    <div>完了</div>
      <ul>
      <li v-for="task in completed_tasks" :key="task.name">
        <div>タスク名: {{ task.name }}</div>
      </li>
    </ul>
    
        <div>
      <label>
         タスク名
        <input v-model="newTaskName" type="text" />
      </label>
      <button @click="addTask">追加</button>
    </div>
    </div>
</template>

<style>
.over500 { 
  color: red; 
} 
</style>