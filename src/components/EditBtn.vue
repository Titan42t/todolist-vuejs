<script setup>
defineProps({
  text: String,
  class: String
})
</script>

<template>
  <button class="editBtn" :class="class">{{ text }}</button>
</template>
