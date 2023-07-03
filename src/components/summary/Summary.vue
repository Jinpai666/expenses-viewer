<template>
  <div class="summary mt-4 pl-4">
    <v-form class="filters d-md-flex align-center justify-center">
      <v-select
          class="w-auto ma-2 pa-2 "
          v-model="select"
          :items="years"
          label="Year"
      ></v-select>
    </v-form>

    <h2 class="summary__title mt-4">Summary</h2>
    <p class="mt-2 pb-2">Total: {{ totalExpenses }} PLN</p>

    <h2>Per period</h2>
    <div class="mt-2" v-for="(total, period) in filteredPeriodSummary" :key="period">
      <p>{{ period }}</p>
      <p>{{ total }} PLN</p>
      <v-divider></v-divider>
    </div>

    <h2 class="summary__title mt-4">Per category</h2>
    <div class="mt-2" v-for="(total, category) in categorySummary" :key="category">
      <p>{{ category }}</p>
      <p>{{ total }} PLN</p>
      <v-divider></v-divider>
    </div>
  </div>
</template>

<script>
import data from "../../data/expenses.json";

export default {
  data() {
    return {
      expenses: data.expenses,
      select: 2023,
      years: [],
    };
  },
  computed: {
    totalExpenses() {
      return this.expenses.reduce((total, expense) => total + expense.amount, 0);
    },
    periodSummary() {
      const summary = {};
      for (const expense of this.expenses) {
        const period = expense.date.substr(0, 7);
        if (summary[period]) {
          summary[period] += expense.amount;
        } else {
          summary[period] = expense.amount;
        }
      }
      return summary;
    },
    filteredPeriodSummary() {
      const selectedYear = this.select;
      if (!selectedYear) return this.periodSummary;

      const filteredSummary = {};
      for (const [period, total] of Object.entries(this.periodSummary)) {
        if (period.startsWith(selectedYear)) {
          filteredSummary[period] = total;
        }
      }
      return filteredSummary;
    },
    categorySummary() {
      const summary = {};
      for (const expense of this.expenses) {
        const category = expense.category;
        if (summary[category]) {
          summary[category] += expense.amount;
        } else {
          summary[category] = expense.amount;
        }
      }
      return summary;
    },

  },
  created() {
    this.years = Array.from(new Set(this.expenses.map((expense) => expense.date.substr(0, 4))));
  },
};
</script>

<style lang="scss" scoped>
@import "summary";
@import "../../../node_modules/@mdi/font/css/materialdesignicons.css";
</style>
