<script setup>
defineProps({
  text: String
})
</script>

<template>
  <button class="editBtn">{{ text }}</button>
</template>
