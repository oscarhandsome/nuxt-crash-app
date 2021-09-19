<template>
  <section>
    <h1>{{ pageTitle }}</h1>

    <ul>
      <li v-for="user of users" :key="user.id">
        <a href="#" @click.prevent="openUser(user)">User {{ user.name }}</a>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data: () => ({
    // users: [],
    pageTitle: 'Users page',
  }),
  async fetch({ store }) {
    if (store.getters['users/users'].length === 0) {
      await store.dispatch('users/fetch')
    }
  },
  // @TODO Move to vuex / Optimization
  // async asyncData({ $axios }) {
  //   const users = await $axios.$get(
  //     'https://jsonplaceholder.typicode.com/users'
  //   )
  //   return { users }
  // },
  computed: {
    users() {
      return this.$store.getters['users/users']
    },
  },
  // @TODO Move to asyncData /  SSR
  // async mounted() {
  //   this.users = await this.$axios.$get(
  //     'https://jsonplaceholder.typicode.com/users'
  //   )
  // },
  methods: {
    openUser(user) {
      this.$router.push('/users/' + user.id)
    },
  },
}
</script>
