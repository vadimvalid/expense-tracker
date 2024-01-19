<template>
  <h3>Your Balance</h3>
  <p>${{ total }}</p>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>
