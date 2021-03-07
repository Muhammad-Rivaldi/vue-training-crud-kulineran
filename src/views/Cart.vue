<template>
  <div class="cart">
    <!-- navbar -->
    <Navbar :updateCart="carts" />
    <!-- end navbar -->

    <div class="container">
      <!-- breadcumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">Cart</li>
            </ol>
          </nav>
        </div>
      </div>
      <!-- end breadcumb -->

      <!-- table -->
      <div class="row">
        <div class="col">
          <h2>My <strong>Cart</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr align="center">
                  <th scope="col">#</th>
                  <th scope="col">Picture</th>
                  <th scope="col">Menu</th>
                  <th scope="col">Description</th>
                  <th scope="col">Price</th>
                  <th scope="col">quantity order</th>
                  <th scope="col">Total Price</th>
                  <th scope="col">Option</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(cart, index) in carts" :key="cart.id">
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/images/' + cart.products.gambar"
                      class="img-fluid shadow"
                    />
                  </td>
                  <td>{{ cart.products.nama }}</td>
                  <td>{{ cart.description ? cart.description : "-" }}</td>
                  <td>Rp {{ cart.products.harga }}</td>
                  <td>{{ cart.order_quantity }}</td>
                  <td>Rp {{ cart.products.harga * cart.order_quantity }}</td>
                  <td align="center" class="text-danger">
                    <b-icon-trash @click="deleteCart(cart.id)"></b-icon-trash>
                  </td>
                </tr>
                <hr />
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total:</strong>
                  </td>
                  <td colspan="2" align="rigth">Rp {{ TotalHarga }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <!-- end table -->

      <!-- form checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-3" v-on:submit.prevent>
            <div class="form-group">
              <label for="name_order">name</label>
              <input
                type="text"
                class="form-control"
                v-model="orders.name_order"
              />
            </div>
            <div class="form-group">
              <label for="table_number">Table Number</label>
              <input
                type="text"
                class="form-control"
                v-model="orders.table_number"
              />
            </div>
            <button
              type="submit"
              class="btn btn-success float-right button_order"
              @click="checkout"
            >
              <b-icon-cart></b-icon-cart> checkout
            </button>
          </form>
        </div>
      </div>
      <!-- end form checkout -->
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "cart",
  components: {
    Navbar,
  },
  data() {
    return {
      carts: {},
      orders: {},
    };
  },
  methods: {
    setCart(data) {
      this.carts = data;
    },
    deleteCart(id) {
      axios.delete("http://localhost:3000/keranjangs/" + id).then(() => {
        this.$toast.error("successful delete the cart", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      });

      // update data cart
      axios
        .get("http://localhost:3000/keranjangs")
        .then((response) => this.setCart(response.data));
    },
    checkout() {
      if (this.orders.name_order && this.orders.table_number) {
        this.orders.carts = this.carts;
        axios.post("http://localhost:3000/pesanans", this.orders).then(() => {
          
          // delete all carts
          this.carts.map(function (item) {
            return axios.delete("http://localhost:3000/keranjangs/" + item.id)
          })

          this.$router.push({ path: "/orderSuccess" });
          this.$toast.success("successful checkout the cart", {
            type: "success",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });
        });
      } else {
        this.$toast.error("the input form cannot be empty", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setCart(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    TotalHarga() {
      return this.carts.reduce(function (item, data) {
        return item + data.products.harga * data.order_quantity;
      }, 0);
    },
  },
};
</script>

<style>
</style>