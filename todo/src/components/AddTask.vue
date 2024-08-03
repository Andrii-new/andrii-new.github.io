<template>
    <h3>Add new Task</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="text">Text*</label>
        <input type="text" id="text" v-model="text" placeholder="Enter text..." />
      </div>
      <div class="form-control">
        <label for="data"
          >Data* <br />
        </label>
      
        <input
          type="text"
          id="data"
          v-model="data"
          placeholder="Enter data and time..."
          
        />
      </div>
      <button class="btn">Add Task</button>
         
    
    </form>
  </template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const text = ref('');
const data = ref('');

const emit = defineEmits(['transactionSubmitted']);

// Get toast interface
const toast = useToast();


const onSubmit = () => {
  if (!text.value || !data.value) {
    // Display a toast error message if either field is empty
    toast.error('Both fields must be filled.');
    return;
  }  
  const transactionData = {
    text: text.value,
    data: data.value,
  };

  emit('transactionSubmitted', transactionData);
  
    // Clear form fields
  text.value = '';
  data.value = '';
};

</script>

