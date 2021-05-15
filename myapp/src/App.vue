<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col">
        <userform></userform>
      </div>
      <div class="col">
        <userdetails></userdetails>
      </div>
    </div>
  </div>
</template>
<script>
import userform from "./components/UserForm.vue";
import userdetails from "./components/UserDetails.vue";
export default {
  name: "App",
  components: {
    userform,
    userdetails,
  },
};
</script>

<style>
</style>
