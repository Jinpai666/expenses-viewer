<template>
  <v-table>
    <thead>
    <tr>
      <th class="text-left">
        Name
      </th>
      <th class="text-left">
        Amount
      </th>
      <th class="text-left">
        Category
      </th>
      <th class="text-left">
        Date
      </th>
      <th class="text-left">
        Time
      </th>
      <th class="text-left">
        Location
      </th>
    </tr>
    </thead>
    <tbody>
    <tr
        v-for="(item, idx) in expenses"
        :key="idx"
    >
      <td>{{ formatString(item.name) }}</td>
      <td>{{ item.amount }} PLN</td>
      <td>{{ formatString(item.category) }}</td>
      <td>{{ formatDate(item.date) }}</td>
      <td>{{ item.time }}</td>
      <td>{{ item.location }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script>
import data from '../data/expenses.json'

export default {
  data() {
    return {
      expenses: data.expenses
    }
  },
  methods: {
    formatString(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    formatDate(date) {
      const formattedDate = new Date(date);
      return formattedDate.toLocaleDateString('pl');
    },
  },
}
</script>