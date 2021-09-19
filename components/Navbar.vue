<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">SSR Nuxt</a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item">
          <nuxt-link
            exact
            no-prefetch
            class="nav-link"
            active-class="active"
            to="/"
            >Home</nuxt-link
          >
        </li>
        <li class="nav-item">
          <nuxt-link class="nav-link" active-class="active" to="/about"
            >About</nuxt-link
          >
        </li>
        <li class="nav-item">
          <nuxt-link class="nav-link" active-class="active" to="/users"
            >Users</nuxt-link
          >
        </li>
        <li v-if="!hasToken" class="nav-item">
          <nuxt-link class="nav-link" active-class="active" to="/login"
            >Login</nuxt-link
          >
        </li>
        <li v-else class="nav-item">
          <a class="nav-link" href="#" @click.prevent="logout"></a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  computed: {
    hasToken() {
      return this.$store.getters.hasToken
    },
  },
  methods: {
    logout() {
      this.$store.dispatch('logout')
      this.$router.push('/login')
    },
  },
}
</script>
