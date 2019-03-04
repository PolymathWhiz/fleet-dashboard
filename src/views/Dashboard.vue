<template>
  <div class="dashboard">
    <div v-if="user_type === 'admin'">
      <Navbar></Navbar>
    </div>
    <div v-else>
      <div class="container">
        <div class="row">
          <div
            class="col-md-6 mr-auto ml-auto"
            style="margin-top: 160px;"
          >
            <button
              type="button"
              class="btn btn-danger"
              style="margin-right: 20px;"
              @click="logout"
            >Logout</button>

            <button
              type="button"
              class="btn btn-primary"
              data-toggle="modal"
              data-target="#exampleModalScrollable"
            >
              Create Booking
            </button>

            <button
              type="button"
              class="btn btn-success"
              style="margin-left: 20px;"
              @click="viewBookings"
            >
              View Bookings
            </button>

            <div
              class="modal fade"
              id="exampleModalScrollable"
              tabindex="-1"
              role="dialog"
              aria-labelledby="exampleModalScrollableTitle"
              aria-hidden="true"
            >
              <div
                class="modal-dialog modal-dialog-scrollable"
                role="document"
              >
                <div class="modal-content">
                  <div class="modal-header">
                    <h5
                      class="modal-title"
                      id="exampleModalScrollableTitle"
                    >Create Booking</h5>
                  </div>
                  <div class="modal-body">
                    <form @submit.prevent="createBooking">
                      <div class="form-group">
                        <label for="exampleInputEmail1">Vehicle type</label>
                        <select
                          class="form-control"
                          v-model="booking.vehicle_type"
                        >
                          <option value="1">Mini</option>
                          <option value="2">Coach</option>
                        </select>

                      </div>
                      <div class="form-group">
                        <label for="exampleInputPassword1">Need date</label>
                        <input
                          type="date"
                          class="form-control"
                          v-model="booking.need_date"
                        >
                      </div>
                      <div class="form-group">
                        <label for="exampleInputPassword1">Reason</label>
                        <input
                          type="text"
                          class="form-control"
                          v-model="booking.reason"
                        >
                      </div>
                      <div class="modal-footer">
                        <button
                          type="button"
                          class="btn btn-secondary"
                          data-dismiss="modal"
                        >Close</button>
                        <button
                          type="submit"
                          class="btn btn-primary"
                        >Create</button>
                      </div>
                    </form>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
</style>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
  components: {
    Navbar
  },
  data() {
    return {
      user_type: "",
      booking: {
        vehicle_type: "",
        need_date: "",
        reason: ""
      }
    };
  },
  methods: {
    async createBooking() {
      try {
        const response = await this.$http.post("/book", {
          token: localStorage.token,
          vehicle_id: this.booking.vehicle_type,
          need_date: this.booking.need_date,
          reason: this.booking.reason
        });

        return alert(response.data.message);
      } catch (error) {
        if (error.response) {
          const message = error.response.data.message;
          return alert(message);
        }
      }
    },
    logout() {
      localStorage.clear();
      this.$router().push({
        path: "/"
      });
    },
    viewBookings() {
      this.$router.push({
        path: "/bookings"
      });
    }
  },
  created() {
    if (!localStorage.token) {
      this.$router.push({
        path: "/"
      });
    }
  }
};
</script>
