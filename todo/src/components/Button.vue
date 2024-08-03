<template>
  <button :style="{ backgroundColor: color }" @click="btnClick" class="close-btn">
    {{ text }}
  </button>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  text: String,
  color: String
});

const emit = defineEmits();

const btnClick = () => {
  emit('btn-click');
};
</script>