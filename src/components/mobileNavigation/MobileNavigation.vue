<template>
  <v-menu >
    <template v-slot:activator="{ props }">
      <v-btn
          class="mobile-menu"
          v-bind="props"
          icon="mdi-menu"
      >
      </v-btn>
    </template>
    <v-list>
      <v-list-item
          v-for="(item, index) in items"
          :key="index"
          :value="index"
      >
        <v-list-item-title>
          <a class="mobile-menu__link" href="#">{{ item.title }}</a>
        </v-list-item-title>
      </v-list-item>
    </v-list>
  </v-menu>
</template>

<script>
export default {
  data: () => ({
    name: "TopNavigation",
    items: [
      { title: 'Dashboard' },
      { title: 'Reports' },
      { title: 'Expenses' },
      { title: 'Settings' },
      { title: 'Profile' },
      { title: 'Logout' },
    ],
  }),
}
</script>

<style lang="scss">
@import "mobileNavigation";
</style>