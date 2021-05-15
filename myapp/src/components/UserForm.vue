<template>
  <div class="card">
    <form @submit.prevent="onPostUser" class="p-5">
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
        <button type="submit" class="btn btn-primary">Add User</button>
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
    };
  },
  methods: {
    onPostUser() {
      axios.post(`http://localhost:3000/users`, {
        id: this.id,
        name: this.name,
        address: this.address,
        pincode: this.pincode,
        phone: this.phone,
      });
      Window.Event.$emit("updateuserdatahandler");
    },
  },
  components: {
    PincodeInput,
    VuePhoneNumberInput,
  },
};
</script>


