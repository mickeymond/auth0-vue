<template>
  <div id="app">
    <h1>Is Logged In: {{ $auth.isAuthenticated }}</h1>

    <div v-if="$auth.isAuthenticated">
      <img height="100" :src="$auth.user.picture">
      <h2>Name: {{ $auth.user.name }}</h2>
      <p>Email: {{ $auth.user.email }}</p>
      <div>
        <pre>{{ JSON.stringify($auth.user, null, 2) }}</pre>
      </div>
    </div>

    <div v-if="!$auth.loading">
      <!-- show login when not authenticated -->
      <button v-if="!$auth.isAuthenticated" @click="login">Log in</button>
      <!-- show logout when authenticated -->
      <button v-if="$auth.isAuthenticated" @click="logout">Log out</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  methods: {
    // Log the user in
    login() {
      this.$auth.loginWithRedirect();
    },
    // Log the user out
    logout() {
      this.$auth.logout();
    }
  },
  watch: {
    '$auth.isAuthenticated': (value) => {
      console.log(value);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
