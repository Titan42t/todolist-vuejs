<script setup>
import EditBtn from './EditBtn.vue';

defineProps({
  item: Object,
  updateTask: Function,
  deleteTask: Function
})


</script>

<template>
  <div class="task">
    <p>{{ item.name }}</p>
    <EditBtn @click="updateTask" text="Éditer"></EditBtn>
    <EditBtn @click="deleteTask(item.name)" text="Supprimer"></EditBtn>
  </div>
</template>
