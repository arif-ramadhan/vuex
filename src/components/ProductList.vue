<template>
  <div class="row">
    <div
      class="card m-4"
      style="width: 15rem"
      v-for="item in products"
      :key="item.id"
    >
      <img class="card-img-top" :src="item.imgUrl" :alt="item.title" />
      <div class="card-body">
        <p class="card-title">{{ item.title }}</p>
        <p class="card-text">
          {{ item.price }}
        </p>
        <a href="#" @click="addToCart(item)" class="btn btn-primary"
          >Add To Cart</a
        >
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "ProductList",
  computed: {
    ...mapGetters(["products"]),
  },
  methods: {
    ...mapActions(["getProducts", "addToCart"]),
  },
  mounted() {
    this.getProducts();
  },
};
</script>

<style scoped>
.row .card {
  border: none;
}
</style>>