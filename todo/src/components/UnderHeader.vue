<template>
    <Button @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'" />
  </template>
  
  <script setup>
  import Button from './Button.vue';
  
  const props = defineProps({
  showAddTask: Boolean
});
  </script>
 