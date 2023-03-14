<script setup>
import EditBtn from './EditBtn.vue';

defineProps({
  item: Object,
  changingTask: Function,
  editingTask: Function,
  updateTask: Function,
  deleteTask: Function
})


</script>

<template>
  <div :id="item.id" class="task">
    <p>{{ item.name }}</p>
    <input :value="item.name">
    <EditBtn @click="editingTask(item.id)" text="Éditer" class="edit"></EditBtn>
    <EditBtn @click="updateTask(item.id)" text="Confirmer" class="confirm"></EditBtn>
    <EditBtn @click="deleteTask(item.name)" text="Supprimer" class="supp"></EditBtn>
  </div>
</template>
