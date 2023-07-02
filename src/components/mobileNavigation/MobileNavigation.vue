<template>
<div>
  top
</div>
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