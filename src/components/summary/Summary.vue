<template>
  <div class="summary mt-4 pl-4">
    <h1 class="section-title mt-8">Summary</h1>

    <v-form class="summary__selection d-md-flex align-center justify-center">
      <v-select
          class="w-auto ma-2 pa-2 "
          v-model="select"
          :items="years"
          label="Year"
      ></v-select>
    </v-form>

    <p class="mt-2 pb-2 summary__accent">Total: {{ totalExpenses }} PLN</p>
<v-row class="mt-4">
  <v-col>
    <h2 class="summary__title">Per period</h2>
    <div class="mt-4" v-for="(total, period) in filteredPeriodSummary" :key="period">
      <p class="summary__accent">{{ period }}</p>
      <p  class="mt-2">{{ total }} PLN</p>
      <v-divider></v-divider>
    </div>
  </v-col>
  <v-col>
    <h2 class="summary__title">Per category</h2>
    <div class="mt-4" v-for="(total, category) in categorySummary" :key="category">
      <p class="summary__accent">{{ category }}</p>
      <p  class="mt-2">{{ total }} PLN</p>
      <v-divider></v-divider>
    </div>
  </v-col>
</v-row>



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
