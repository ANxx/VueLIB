<template>
  <div class="container">
    <form class="row g-3" @submit.prevent="CreateUser">
      <div class="col-md-6">
        <label for="inputEmail4" class="form-label">First name</label>
        <input
          type="text"
          name="first_name"
          v-model="first_name"
          class="form-control"
          id="inputEmail4"
        />
      </div>
      <div class="col-md-6">
        <label for="inputPassword4" class="form-label">Last Name</label>
        <input
          type="text"
          name="last_name"
          v-model="last_name"
          class="form-control"
          id="inputPassword4"
        />
      </div>
      <div class="col-md-6">
        <label for="inputEmail4" class="form-label">Email</label>
        <input
          type="email"
          name="email"
          v-model="email"
          class="form-control"
          id="inputEmail4"
        />
      </div>
      <div class="col-md-6">
        <label for="inputPassword4" class="form-label">Username</label>
        <input
          type="text"
          name="username"
          v-model="username"
          class="form-control"
          id="inputPassword4"
        />
      </div>
      <div class="col-md-6">
        <label for="inputEmail4" class="form-label">Password</label>
        <input
          type="password"
          name="password"
          v-model="password"
          class="form-control"
          id="inputEmail4"
        />
      </div>
      <div class="col-md-6">
        <label for="inputPassword4" class="form-label">Confirm Password</label>
        <input
          type="password"
          name="password2"
          v-model="password2"
          class="form-control"
          id="inputPassword4"
        />
      </div>

      <div class="col-12">
        <button type="submit" class="btn btn-primary">Sign in</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "register",
  components: {},
  data() {
    return {
      first_name: null,
      last_name: null,
      email: null,
      username: null,
      password: null,
      password2: null,
    };
  },
  methods: {
    CreateUser() {
      console.log(
        this.username,
        this.first_name,
        this.last_name,
        this.email,
        this.username,
        this.password,
        this.password2
      );
      axios
        .post("http://127.0.0.1:8000/api/register/", {
          username: this.username,
          email: this.email,
          password: this.password,
          password2: this.password2,
          first_name: this.first_name,
          last_name: this.last_name,
        })
        .then((res) => {
          console.log(res);
          this.$router.push("/");
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>