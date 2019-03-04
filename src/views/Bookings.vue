<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Vehicle Type</th>
              <th scope="col">Need date</th>
              <th scope="col">Reason</th>
              <th scope="col">Confirmed</th>
              <th scope="col">Created</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="booking in bookings"
              v-bind:key="booking.id"
            >
              <th scope="row">{{ booking.id }}</th>
              <td>{{ booking.vehicle_id }}</td>
              <td>{{ new Date(booking.need_date).toDateString() }}</td>
              <td> {{ booking.reason }}</td>
              <td>{{ booking.is_confirmed }}</td>
              <td>{{ new Date(booking.created_at).toDateString() }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style>
</style>

<script>
export default {
  data() {
    return {
      bookings: []
    };
  },
  methods: {
    async getBookings() {
      try {
        const response = await this.$http.get(
          `/book/?token=${localStorage.token}`
        );

        console.log(response.data.data);

        for (let i = 0; i < response.data.data.length; i++) {
          this.bookings.push(response.data.data[i]);
        }
      } catch (error) {
        if (error.response) {
          const message = error.response.data.message;
          return alert(message);
        }
      }
    }
  },
  created() {
    this.getBookings();
    console.log(this.bookings);
  }
};
</script>
