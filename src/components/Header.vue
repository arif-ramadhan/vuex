<template>
  <nav class="navbar navbar-light bg-success">
    <a class="navbar-brand" href="#"> SHOPPING </a>
    <a class="navbar-brand" href="#"> Cart ({{ totalQty }}) </a>
  </nav>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  name: "Header",
  computed: {
    ...mapGetters(["cart"]),
    totalQty() {
      return this.cart.reduce((a, b) => a + b.qty, 0);
    },
  },
};
</script>>