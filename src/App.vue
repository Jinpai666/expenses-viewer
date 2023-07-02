<script setup lang="ts">
import ExpensesTable from "./components/expensesTable/ExpensesTable.vue";
import MobileNavigation from "./components/mobileNavigation/MobileNavigation.vue";
import TopNavigation from "./components/topNavigation/TopNavigation.vue";
</script>

<template>
  <VContainer class="container">
    <h1>Expenses Table</h1>
    <TopNavigation/>
    <MobileNavigation/>
    <ExpensesTable />
  </VContainer>

</template>

<style scoped>
  .container{
    max-width: 1200px !important;
  }
  h1{
    font-family: 'Catamaran', sans-serif;
    font-weight: bold;
    font-size: 36px;
    text-align: center;
  }
</style>
