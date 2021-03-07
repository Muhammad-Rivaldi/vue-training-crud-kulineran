<template>
  <div class="order-success">
    <Navbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img src="../assets/images/Hero.png" width="25%">
          <h2 class="mt-3"><strong>Success!!</strong></h2>
          <h4>your order is being processed <br> please wait</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
// import axios from "axios";

export default {
  name: "orderSuccess",
  components: {
    Navbar
  }
};
</script>

<style>
</style>