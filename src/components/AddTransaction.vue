<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="text" type="text" id="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        v-model="amount"
        type="text"
        id="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const amount = ref("");
const toast = useToast();
const emit = defineEmits(["add-transaction"]);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both fields must be filled");
  } else {
    const newTransaction = {
      id: Math.floor(Math.random() * 100000000),
      text: text.value,
      amount: +amount.value,
    };

    emit("add-transaction", newTransaction);
  }

  text.value = "";
  amount.value = "";
};
</script>
