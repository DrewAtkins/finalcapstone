<template>
  <div>
    <header-area />
    <logged-in-view />
    <div class="container">
      <div
        class="pending-apps"
        v-if="$store.state.user.authorities[0].name === 'ROLE_ADMIN'"
      >
        <router-link
          v-bind:to="{ name: 'pending-volunteer-list' }"
          class="links"
          >See Pending Volunteer Applications</router-link
        >
        <hr />
      </div>
      <table id="tblUsers">
        <thead>
          <tr>
            <th>Employee Name</th>
            <th>Email Address</th>
            <th>Phone #</th>
            <th>Role</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in $store.state.users" v-bind:key="user.id">
            <td>{{ user.full_name }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td>{{ user.authorities[0].name }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <footer-area />
  </div>
</template>

<script>
import userService from "@/services/UserService.js";
import HeaderArea from "@/components/HeaderArea.vue";
import FooterArea from "@/components/FooterArea.vue";
import LoggedInView from "../views/LoggedInView.vue";

export default {
  components: { HeaderArea, FooterArea, LoggedInView },
  created() {
    userService.displayDirectory().then((response) => {
      this.$store.state.users = response.data;
    });
  },
};
</script>


<style scoped>
table {
  margin: 20px auto 20px;
  width: 75%;
}

th {
  text-transform: uppercase;
  text-align: left;
}

td {
  padding: 10px 0px 10px;
}

input,
select {
  font-size: 16px;
}

form {
  margin: 20px;
  width: 350px;
}

.field {
  padding: 10px 0px;
}

label {
  width: 140px;
  display: inline-block;
}

.pending-apps {
  text-align: center;
  text-transform: uppercase;
  font-weight: bold;
  margin-top: 5px;
}
</style>