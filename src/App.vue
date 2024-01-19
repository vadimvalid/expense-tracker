<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="income" :expense="expense" />
    <TransactionList
      :transactions="transactions"
      @deleteTransaction="handleDeleteTransaction"
    />
    <AddTransaction @addTransaction="handleSubmit" />
  </div>
</template>

<script setup>
import { computed, ref, onMounted } from "vue";
import { useToast } from "vue-toastification";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const transactions = ref([]);
const toast = useToast();

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// Get total
const total = computed(() => {
  return transactions.value
    .map((t) => t.amount)
    .reduce((acc, item) => (acc += item), 0);
});

// Get Income
const income = computed(() => {
  return Number(
    transactions.value
      .filter((t) => t.amount > 0)
      .reduce((acc, item) => acc + item.amount, 0)
      .toFixed(2)
  );
});

// Get Expense
const expense = computed(() => {
  return Number(
    transactions.value
      .filter((t) => t.amount < 0)
      .reduce((acc, item) => acc + item.amount, 0)
      .toFixed(2)
  );
});

// Add Transaction
const handleSubmit = (newTransaction) => {
  transactions.value = [...transactions.value, newTransaction];

  saveTransactionToLocalStorage();
  toast.success("Transaction added");
};

// Delete Transaction
const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter((t) => t.id !== id);

  saveTransactionToLocalStorage();
  toast.success("Transaction deleted");
};

// Save to localstorage
const saveTransactionToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>
