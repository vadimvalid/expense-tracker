<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpense />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const transactions = ref([
  { id: 1, text: "Cash", amount: -400 },
  { id: 2, text: "Paycheck", amount: 900 },
]);
</script>
