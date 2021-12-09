<template>
  <div>
    <nav class="navbar navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand">Vue DJANGO API</a>
        <form @submit.prevent="logout" v-if="token !== null">
            <button class="btn btn-outline-success" type="submit">Logout</button>
        </form>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Header",
  component: {},
  data() {
    return {
      token: localStorage.getItem("user-token") || null,
    };
  },
  methods: {
    logout() {
      localStorage.removeItem("user-token");
      localStorage.removeItem("is_admin");
      localStorage.removeItem("first_name")
      this.token = null;
      this.$router.push("/");
    },

  },
};
</script>