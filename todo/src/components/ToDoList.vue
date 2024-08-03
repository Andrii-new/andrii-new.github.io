<template>
    <h3>Task</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.data">
            {{ transaction.text }} <span>{{ transaction.data }}</span><button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
                
    </ul>
</template>


<script setup>
import {defineProps} from 'vue';

const props = defineProps({
    transactions: {
        type: Array,
        requered: true,
    },
});

const emit = defineEmits(['transactionDeleted']);
    
const deleteTransaction = (id) => {
  emit('transactionDeleted', id);
};

</script>