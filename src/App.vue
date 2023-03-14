<script setup>
import NewTaskComponent from './components/NewTask.vue'
import TaskComponent from './components/Task.vue'
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])
var currentIndex = 2

function addTask() {
  tasks.value.push({id: 'div'+(currentIndex + 1), name: newTask.value})
  newTask.value = ''
  currentIndex++
}

function update(e) {
  newTask.value = e.target.value
}

function editingTask(id) {
  //On transforme la balise <p> en <input>
  const pElement = document.querySelector('#'+id+' p')
  const input = document.querySelector('#'+id+' input')
  pElement.style.display = 'none'
  input.style.display = 'block'

  //On transforme le bouton "Editer" en "Confirmer"
  const editBtn = document.querySelector('#'+id+' .edit')
  const confirmBtn = document.querySelector('#'+id+' .confirm')
  editBtn.style.display = 'none'
  confirmBtn.style.display = 'block'
}

function updateTask(id) {
  //On transforme la balise <input> en <p>
  const pElement = document.querySelector('#'+id+' p')
  const input = document.querySelector('#'+id+' input')
  pElement.style.display = 'block'
  input.style.display = 'none'

  //On transforme le bouton "Confirmer" en "Editer"
  const editBtn = document.querySelector('#'+id+' .edit')
  const confirmBtn = document.querySelector('#'+id+' .confirm')
  editBtn.style.display = 'block'
  confirmBtn.style.display = 'none'

  //On met à jour la valeur de notre item
  const index = tasks.value.findIndex(element => element.id == id)
  tasks.value[index].name = input.value
  console.log(tasks.value)
}

function deleteTask(param) {
  const index = tasks.value.findIndex(element => element.name == param)
  tasks.value.splice(index, 1)
}

function deleteAll() {
  tasks.value=[]
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
        :editingTask="editingTask"
        :updateTask="updateTask"
        :deleteTask="deleteTask"
        :key="item.id"
      ></TaskComponent>
      <button class="deleteAll" @click="deleteAll">Tout supprimer</button>
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
p {
  margin: 0;
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
  padding: 5px;
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
  margin: 10px 0;
}
.task input {
  display: none;
}
.task .editBtn {
  height: fit-content;
  background: rgb(179, 179, 179);
  padding: 5px 10px;
}
.task .confirm {
  display: none;
}
.deleteAll {
  background: rgb(255, 72, 72);
  color: white;
}
</style>
