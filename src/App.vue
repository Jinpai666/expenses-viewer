<script setup lang="ts">
import ExpensesTable from "./components/expensesTable/ExpensesTable.vue";
import MobileNavigation from "./components/mobileNavigation/MobileNavigation.vue";
import TopNavigation from "./components/topNavigation/TopNavigation.vue";
import Summary from "./components/summary/Summary.vue";
</script>

<template>
  <VContainer class="container">
    <TopNavigation/>
    <MobileNavigation/>
    <ExpensesTable />
    <Summary/>
  </VContainer>

</template>

<style >
@import "./style.scss";
@import "./reset.scss";


</style>
