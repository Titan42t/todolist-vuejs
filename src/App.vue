<script setup>
import NewTaskComponent from './components/NewTask.vue'
import TaskComponent from './components/Task.vue'
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([{
    id: 1,
    name: 'Tâche 1'
  },
  {
    id: 2,
    name: 'Tâche 2'
  }
])

function addTask() {
  tasks.value.push({id: tasks.value.length + 1, name: newTask.value})
  newTask.value = ''
}

function update(e) {
  newTask.value = e.target.value
}

function updateTask() {

}

function deleteTask(param) {
  const index = tasks.value.findIndex(element => element.name == param)
  tasks.value.splice(index, 1)
}
</script>

<template>
  <div class="app">
    <h1 class="title">To Do List</h1>
    <NewTaskComponent :props="{newTask, addTask, update}"></NewTaskComponent>
    <div class="list">
      <h2>Ma liste :</h2>
      <TaskComponent v-for="item of tasks"
        :item="item"
        :updateTask="updateTask"
        :deleteTask="deleteTask"
        :key="item.id"
      ></TaskComponent>
    </div>
  </div>
</template>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: unset;
}
.app {
  background-color: black;
  padding: 20px;
  width: 60%;
}
.title {
  background: rgb(62, 197, 255);
  color: white;
  font-size: 30px;
  font-weight: 700;
  padding: 5px 0;
  margin: 0;
  margin-bottom: 10px;
}
.newTask {
  margin-bottom: 15px;
}
.newTask .addBtn {
  background: rgb(62, 197, 255);
  color: white;
  padding: 5px 20px;
  border-radius: 10px;
  margin-left: 10px;
}
.list {
  background: white;
  width: 70%;
  margin: 0 auto;
}

.list h2 {
  font-size: 24px;
  font-weight: 400;
  margin: 0;
  margin-bottom: 15px;
}
.list .task {
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 10px;
}
.list .task .editBtn {
  height: fit-content;
  background: rgb(179, 179, 179);
  padding: 5px 10px;
}
</style>
