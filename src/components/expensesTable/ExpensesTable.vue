<template>
  <div>
    <h1 class="section-title">Expenses Table</h1>

    <div class="expenses">
      <v-form class="filters d-md-flex align-center justify-center">
        <div
          class="position-relative filters__date-picker w-auto ma-2 pa-2 rounded-tse"
        >
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
          class="ma-2 pa-2"
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
            v-for="(item, idx) in paginatedExpenses"
            :key="idx"
          >
            <td class="table-cell">{{ formatString(item.name) }}</td>
            <td  class="table-cell">{{ item.amount }} PLN</td>
            <td class="table-cell mobile-hidden">{{ formatString(item.category) }}</td>
            <td class="table-cell">{{ formatDate(item.date) }}</td>
            <td class="table-cell mobile-hidden">{{ item.time }}</td>
            <td class="table-cell mobile-hidden">{{ item.location }}</td>
          </tr>
        </tbody>
      </v-table>
    </div>
    <div class="pagination">
      <button
        class="pagination__button"
        :disabled="currentPage === 1"
        @click="previousPage"
      >
        Previous
      </button>
      <span class="pagination__info">{{ currentPage }} / {{ totalPages }}</span>
      <button
        class="pagination__button"
        :disabled="currentPage === totalPages"
        @click="nextPage"
      >
        Next
      </button>
    </div>
  </div>
</template>
<style lang="scss">
@import "expensesTable";
@import "../../../node_modules/@mdi/font/css/materialdesignicons.css";

.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}

.pagination__button {
  margin: 0 5px;
}

.pagination__info {
  margin: 0 10px;
}
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
    itemsPerPage: 5,
    currentPage: 1,
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
    totalPages() {
      return Math.ceil(this.filteredExpenses.length / this.itemsPerPage);
    },
    paginatedExpenses() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.filteredExpenses.slice(startIndex, endIndex);
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
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },

    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
  },
};
</script>
