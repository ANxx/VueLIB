<template>
  <div class="container py-5 h-100">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col-12 col-md-8 col-lg-6 col-xl-5">
        <div class="card shadow-2-strong" style="border-radius: 1rem">
          <div class="card-body p-5 text-center">
            <h3 class="mb-5">Sign in</h3>

            <div class="form-outline mb-4">
              <input
                type="email"
                id="typeEmailX-2"
                v-model="username"
                class="form-control form-control-lg"
              />
              <label class="form-label" for="typeEmailX-2">Username</label>
            </div>

            <div class="form-outline mb-4">
              <input
                type="password"
                id="typePasswordX-2"
                v-model="password"
                class="form-control form-control-lg"
              />
              <label class="form-label" for="typePasswordX-2">Password</label>
            </div>
            <div class="row">
              <div class="col">
                <button
                  @click="login"
                  class="btn btn-primary btn-lg btn-block"
                  type="submit"
                >
                  Login
                </button>
              </div>
              <div class="col">
                <form @submit.prevent="register">
                  <button
                    class="btn btn-secondary btn-lg btn-block"
                    type="submit"
                  >
                    Register
                  </button>
                </form>
              </div>
            </div>

            <hr class="my-4" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  components: {},
  data() {
    return {
      username: "",
      password: "",
      first_name:"",
      is_admin: null,
    };
  },

  methods: {
    login() {
      axios
        .post("http://127.0.0.1:8000/auth/", {
          username: this.username,
          password: this.password,
        })
        .then((resp) => {
          // this.token = resp.data.token;
          // this.is_admin = resp.data.is_admin;
          // console.log(this.token, this.is_admin);
          localStorage.setItem("user-token", resp.data.token);
          localStorage.setItem("is_admin", resp.data.is_admin);
          localStorage.setItem("first_name", resp.data.first_name);


          this.$router.push("/lib");
        })
        .catch((err) => {
          localStorage.removeItem("user-token");
        });
    },
    register() {
      this.$router.push("/register");
      console.log("Router");
    },
  },
};
</script>