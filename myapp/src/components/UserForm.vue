<template>
  <div class="card">
    <form @submit.prevent="submitUserData" class="p-5">
      <div class="form-group">
        <input
          type="text"
          placeholder="name"
          class="form-control"
          v-model="name"
          required
        />
      </div>
      <div class="form-group">
        <input
          type="text"
          placeholder="address"
          class="form-control"
          v-model="address"
          required
        />
      </div>
      <div class="form-group">
        <label class="col">Pincode : </label>
        <PincodeInput
          v-model="pincode"
          placeholder="0"
          :autofocus="false"
          :length="6"
        />
      </div>
      <div class="form-group">
        <VuePhoneNumberInput v-model="phone" />
      </div>
      <div class="form-group mt-4">
        <button type="submit" class="btn btn-primary">{{ button }}</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import PincodeInput from "vue-pincode-input";
import VuePhoneNumberInput from "vue-phone-number-input";
import "vue-phone-number-input/dist/vue-phone-number-input.css";

export default {
  data() {
    return {
      id: 0,
      name: "",
      address: "",
      pincode: "",
      phone: "",
      button: "Add User",
    };
  },
  mounted() {
    Window.Event.$on("edituserdata", (id) => {
      this.editUserData(id);
    });
  },
  methods: {
    submitUserData() {
      if (this.button == "Add User") {
        axios
          .post(`http://localhost:3000/users`, {
            id: this.id,
            name: this.name,
            address: this.address,
            pincode: this.pincode,
            phone: this.phone,
          })
          .catch((error) => {
            console.log(error);
          });
      } else {
        axios
          .put(`http://localhost:3000/users/` + this.id + `/`, {
            id: this.id,
            name: this.name,
            address: this.address,
            pincode: this.pincode,
            phone: this.phone,
          })
          .catch((error) => {
            console.log(error);
          });
        this.button = "Add User";
      }
      this.name = "";
      this.address = "";
      this.pincode = "";
      this.phone = "";
      this.button = "Add User";
      Window.Event.$emit("updateuserdatahandler");
    },
    editUserData(id) {
      axios
        .get(`http://localhost:3000/users/` + id)
        .then((response) => {
          this.id = response.data.id;
          this.name = response.data.name;
          this.address = response.data.address;
          this.pincode = response.data.pincode;
          this.phone = response.data.phone;
          this.button = "Update User";
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  components: {
    PincodeInput,
    VuePhoneNumberInput,
  },
};
</script>


