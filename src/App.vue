<script setup lang="ts">
import ExpensesTable from "./components/expensesTable/ExpensesTable.vue";
import MobileNavigation from "./components/mobileNavigation/MobileNavigation.vue";
import TopNavigation from "./components/topNavigation/TopNavigation.vue";
</script>

<template>
  <VContainer class="container">
    <TopNavigation/>
    <MobileNavigation/>
    <ExpensesTable />
  </VContainer>

</template>

<style scoped>
  .container{
    max-width: 1200px !important;
  }
</style>
