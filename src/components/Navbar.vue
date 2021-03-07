<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">kulineran</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/foods">Foods</router-link>
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <router-link class="nav-link" to="/cart">
              Cart
              <b-icon icon="bag"></b-icon>
              <span class="badge badge-success bag ml-1">{{
                updateCart ? updateCart.length : quantity_orders.length
              }}</span>
            </router-link>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "navbar",
  data() {
    return {
      quantity_orders: [],
    };
  },
  props: ["updateCart"],
  methods: {
    setQuantity(data) {
      this.quantity_orders = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setQuantity(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>