<template>
  <div class="container">
    <div class="row">
      <div
        class="col-md-6 mr-auto ml-auto"
        style="margin-top: 60px;"
      >
        <form @submit.prevent="login">
          <div class="form-group">
            <label for="exampleInputEmail1">Email</label>
            <input
              type="email"
              v-model="email"
              class="form-control"
              required
            >
          </div>
          <div class="form-group">
            <label for="exampleInputPassword1">Password</label>
            <input
              type="password"
              v-model="password"
              class="form-control"
              required
            >
          </div>
          <button
            type="submit"
            class="btn btn-primary btn-block"
          >Submit</button>
        </form>

        <p
          class="text-muted text-center"
          style="margin-top: 30px;"
        >Don't have an account? <router-link to="/register">Sign up</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>

<script>
export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    async login() {
      try {
        const response = await this.$http.post("/auth/login", {
          email: this.email,
          password: this.password
        });
        // save data to localstorage
        localStorage.clear();
        localStorage.setItem("loggedIn", true);
        localStorage.setItem("token", response.data.data.token);
        localStorage.setItem("partner", JSON.stringify(response.data.data));
        // move to next page
        this.$router.push({
          path: "/dashboard"
        });
      } catch (error) {
        if (error.response) {
          const message = error.response.data.message;
          alert(message);
        }
      }
    }
  }
};
</script>
