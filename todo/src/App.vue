<template>
  <MainHeader />
  <div class="container">
    <ToDoList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
      <div v-show="showAddTask">
        <AddTask @transactionSubmitted="handleTransactionSubmitted" />
      </div>
  </div>
  <UnderHeader :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" />

</template>

<script setup>
import MainHeader from './components/MainHeader.vue';
import ToDoList from './components/ToDoList.vue';
import AddTask from './components/AddTask.vue';
import UnderHeader from './components/UnderHeader.vue';




import { useToast } from 'vue-toastification';

import {ref, onMounted} from 'vue';

const toast = useToast();

const transactions = ref([]);

const showAddTask = ref(true);



onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    data: transactionData.data,
  });

  saveTransactionsToLocalStorage();

toast.success('Task added.');
};

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success('Task deleted.');
};

// Save transactions to local storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};

const toggleAddTask = () => {
  showAddTask.value = !showAddTask.value

};

</script>
