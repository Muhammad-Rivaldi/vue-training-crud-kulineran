<template>
  <div class="hero">
    <!-- for desktop -->
    <div class="d-none d-md-block">
      <div class="row mt-1">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious food menu,</strong><br />
                in your gadget
              </h2>
              <p>let's immediately select and order your favorite food</p>
              <router-link class="btn btn-lg btn-success button" to="/foods">
                <b-icon-arrow-right></b-icon-arrow-right> choose your food
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/images/ilustrasi.png" width="100%" />
        </div>
      </div>
    </div>
    <!-- end for desktop -->

    <!-- for mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-1">
        <div class="col-md-6 mb-3">
          <img src="../assets/images/ilustrasi.png" width="100%" />
        </div>
        <div class="col-md-6 ">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious food menu,</strong><br />
                in your gadget
              </h2>
              <p>let's immediately select and order your favorite food</p>
              <button class="btn btn-lg btn-success button">
                <b-icon-arrow-right></b-icon-arrow-right> choose your food
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- end for mobile -->
  </div>
</template>

<script>
export default {
  name: "hero",
};
</script>

<style>
</style>