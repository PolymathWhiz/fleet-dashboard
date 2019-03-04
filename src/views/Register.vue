<template>
  <div class="container">
    <div class="row">
      <div
        class="col-md-6 mr-auto ml-auto"
        style="margin-top: 60px;"
      >
        <form @submit.prevent="register">
          <div class="form-group">
            <label for="exampleInputEmail1">First Name</label>
            <input
              type="text"
              v-model="first_name"
              class="form-control"
              required
            >
          </div>

          <div class="form-group">
            <label for="exampleInputEmail1">Last Name</label>
            <input
              type="text"
              v-model="last_name"
              class="form-control"
              required
            >
          </div>

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
        >Already have an account? <router-link to="/">Login</router-link>
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
      first_name: "",
      last_name: "",
      email: "",
      password: ""
    };
  },
  methods: {
    async register() {
      try {
        const response = await this.$http.post("/auth/register", {
          email: this.email,
          password: this.password,
          first_name: this.first_name,
          last_name: this.last_name
        });
        // save data to localstorage
        localStorage.clear();
        localStorage.setItem("loggedIn", true);
        localStorage.setItem("token", response.data.data.token);
        localStorage.setItem("user_data", JSON.stringify(response.data.data));
        // move to next page
        this.$router.push({
          path: "/dashboard"
        });
      } catch (error) {
        if (error.response) {
          const message = error.response.data.message;
          return alert(message);
        }
      }
    }
  }
};
</script>
