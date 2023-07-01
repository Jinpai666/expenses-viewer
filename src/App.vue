<script setup lang="ts">
import ExpensesTable from "./components/ExpensesTable.vue";
</script>

<template>
  <VContainer class="container">
    <div>TopNav</div>
    <ExpensesTable />
  </VContainer>

</template>

<style scoped>
  .container{
    max-width: 1200px !important;
  }
</style>
