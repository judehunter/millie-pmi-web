<template>
  <main class="padded-container">
    <UserCard v-for="(user, idx) in users" :key="idx" :user="user" />
  </main>
</template>

<script>
export default {
  layout: 'admin',
  data() {
    return {
      users: []
    }
  },
  async fetch() {
    this.users = await this.$axios.$get('users');
  }
}
</script>

<style lang="scss" scoped>
h1 {
  font-size: 2rem;
  font-weight: bold;
  margin: .3em 0;
}
h2 {
  font-size: 1.4rem;
  font-weight: bold;
  margin: .3em 0;
}
</style>
