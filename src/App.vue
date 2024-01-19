<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="income" :expense="expense" />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const transactions = ref([
  { id: 1, text: "Cash", amount: -400 },
  { id: 2, text: "Paycheck", amount: 900 },
  { id: 3, text: "Camera", amount: -123.5 },
]);

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
</script>
