<template>
  <table class="table table-striped table-bordered">
    <thead>
      <tr>
        <th>Id</th>
        <th>Name</th>
        <th>Address</th>
        <th>Pincode</th>
        <th>Phone</th>
        <th>Update</th>
        <th>Delete</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.id }}</td>
        <td>{{ user.name }}</td>
        <td>{{ user.address }}</td>
        <td>{{ user.pincode }}</td>
        <td>{{ user.phone }}</td>
        <td>
          <button class="btn btn-warning" @click="editUserData(user.id)">
            Edit
          </button>
        </td>
        <td>
          <button class="btn btn-info" @click="deleteUserData(user.id)">
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    this.getUserData();
    Window.Event.$on("updateuserdatahandler", () => {
      this.getUserData();
    });
  },
  methods: {
    getUserData() {
      axios
        .get(`http://localhost:3000/users`)
        .then((response) => {
          this.users = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    deleteUserData(id) {
      axios.delete(`http://localhost:3000/users/` + id).catch((error) => {
        console.log(error);
      });
      this.getUserData();
    },
    editUserData(id) {
      Window.Event.$emit("edituserdata", id);
    },
  },
};
</script>