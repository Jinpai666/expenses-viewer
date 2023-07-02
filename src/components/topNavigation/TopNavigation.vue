<template>
  <div class="navigation">
    <ul class="navigation__list navigation__list_left">
      <li class="navigation__item" v-for="(item, index) in leftItems" :key="index">
        <a class="navigation__link" href="#"></a>
        {{ item.title }}
      </li>
    </ul>
    <ul class="navigation__list navigation__list_right">
      <li class="navigation__item" v-for="(item, index) in rightItems" :key="index">
        <a class="navigation__link" href=""></a>
        {{ item.title }}
      </li>
    </ul>
  </div>

</template>

<script>
export default {
  data: () => ({
    name: "TopNavigation",
    leftItems: [
      { title: 'Dashboard' },
      { title: 'Reports' },
      { title: 'Expenses' },
      { title: 'Settings' },

    ],
    rightItems: [
      { title: 'Profile' },
      { title: 'Logout' },
    ],
  }),
}
</script>

<style lang="scss">
@import "topNavigation";
</style>