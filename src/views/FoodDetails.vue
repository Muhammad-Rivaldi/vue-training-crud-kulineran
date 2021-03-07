<template>
  <div class="food-detail">
    <Navbar />
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
              <li class="breadcrumb-item active" aria-current="page">
                Food Detail
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <!-- end breadcumb -->

      <div class="row mt-2">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Price <strong> Rp {{ product.harga }}</strong>
          </h4>

          <!-- form -->
          <form class="mt-3" v-on:submit.prevent>
            <div class="form-group">
              <label for="order_quantity">order quantity</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.order_quantity"
              />
            </div>
            <div class="form-group">
              <label for="description">description</label>
              <textarea
                v-model="pesan.description"
                class="form-control"
                placeholder="description"
              ></textarea>
            </div>
            <button
              type="submit"
              class="btn btn-success button_order"
              @click="pemesanan"
            >
              <b-icon-cart></b-icon-cart> Order
            </button>
          </form>
          <!-- end form -->

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetails",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.order_quantity) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({path: "/cart"})
            this.$toast.success("successful order and enter the cart", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
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
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>