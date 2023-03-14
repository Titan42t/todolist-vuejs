<script setup>
defineProps({
  props: Object
})
</script>

<template>
  <div class="newTask">
    <input placeholder="Add Task..." @input="props.update" :value="props.newTask">
    <button class="addBtn" @click="props.addTask">Valider</button>
  </div>
</template>
