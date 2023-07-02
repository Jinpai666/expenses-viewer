<template>
  <div>
    <div>
      <v-form
        class="filters d-md-flex align-center justify-center"
      >
        <div class="position-relative filters__date-picker w-auto ma-2 pa-2 rounded-tse">
          <div class="text-center">Period</div>
          <label>
            <span class="d-flex flex-wrap align-center justify-center">
              <input
                class="ma-2 pa-2 rounded filters__date"
                type="date"
                v-model="startDate" />
              <input
                class="ma-2 pa-2 rounded filters__date"
                type="date"
                v-model="endDate" /></span
          ></label>
          <v-btn
            density="compact"
            icon="mdi-close-circle"
            class="position-absolute filters__button rounded-xl"
            @click="clearDateFilters"
            v-if="this.endDate || this.startDate"
          ></v-btn>
        </div>
        <v-select
          class="w-auto ma-2 pa-2"
          v-model="select"
          :items="['food', 'car']"
          label="Category"
          clearable
        ></v-select>
        <v-text-field
          class="  ma-2 pa-2"
          v-model="searchPhrase"
          :counter="20"
          label="Search by name"
          required
          clearable

        ></v-text-field>
      </v-form>
      <v-table>
        <thead>
          <tr>
            <th class="text-center">Name</th>
            <th class="text-center">Amount</th>
            <th class="mobile-hidden text-center">Category</th>
            <th class="text-center">Date</th>
            <th class="mobile-hidden text-center">Time</th>
            <th class="mobile-hidden text-center">Location</th>
          </tr>
        </thead>
        <tbody>
          <tr
            class="text-center table-row"
            v-for="(item, idx) in filteredExpenses"
            :key="idx"
          >
            <td>{{ formatString(item.name) }}</td>
            <td>{{ item.amount }} PLN</td>
            <td class="mobile-hidden">{{ formatString(item.category) }}</td>
            <td class="">{{ formatDate(item.date) }}</td>
            <td class="mobile-hidden">{{ item.time }}</td>
            <td class="mobile-hidden">{{ item.location }}</td>
          </tr>
        </tbody>
      </v-table>
    </div>
  </div>
</template>
<style lang="scss">
@import "expensesTable";
@import "../../../node_modules/@mdi/font/css/materialdesignicons.css";
</style>
<script>
import data from "../../data/expenses.json";

export default {
  data: () => ({
    select: null,
    expenses: data.expenses,
    searchPhrase: "",
    startDate: "",
    endDate: "",
  }),
  computed: {
    filteredExpenses() {
      let filteredArray = this.expenses;

      if (this.select) {
        filteredArray = filteredArray.filter(
          (item) => item.category === this.select
        );
      }

      if (this.searchPhrase) {
        const searchRegex = new RegExp(this.searchPhrase, "i");
        filteredArray = filteredArray.filter((item) =>
          searchRegex.test(item.name)
        );
      }

      if (this.startDate) {
        filteredArray = filteredArray.filter(
          (item) => new Date(item.date) >= new Date(this.startDate)
        );
      }
      if (this.endDate) {
        filteredArray = filteredArray.filter(
          (item) => new Date(item.date) <= new Date(this.endDate)
        );
      }

      return filteredArray;
    },
  },
  methods: {
    formatString(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    formatDate(date) {
      const formattedDate = new Date(date);
      return formattedDate.toLocaleDateString("pl");
    },
    clearDateFilters() {
      this.startDate = "";
      this.endDate = "";
    },
  },
};
</script>
