<template>
  <div class="m-4">
    <div v-if="!cart.length" class="alert alert-warning" role="alert">
      Cart is empty
    </div>
    <div v-if="orderPlace" class="alert alert-success" role="alert">
      <button
        @click="() => (orderPlace = false)"
        type="button"
        class="close"
        data-dismiss="modal"
        aria-label="Close"
      >
        <span aria-hidden="true">&times;</span>
      </button>
      Product has been placed
    </div>
    <ul class="list-group" v-for="item in cart" :key="item.id">
      <li class="list-group-item">
        <button
          @click="removeItem(item.id)"
          type="button"
          class="close"
          data-dismiss="modal"
          aria-label="Close"
        >
          <span aria-hidden="true">&times;</span>
        </button>
        <div class="media">
          <img width="80px" class="mr-3" :src="item.imgUrl" :alt="item.title" />
          <div class="media-body">
            <p class="mt-0">{{ item.title }}</p>
            <button
              @click="reduceQty(item.id)"
              class="btn-qty btn btn-sm btn-info"
            >
              -
            </button>
            x {{ item.qty }}
            <button
              @click="addQty(item.id)"
              class="btn-qty btn btn-sm btn-info"
            >
              +
            </button>
          </div>
        </div>
      </li>
    </ul>
    <button
      @click="PlaceOrder"
      v-if="cart.length"
      class="btn btn-success btn-lg btn-block mt-3"
      :disabled="isProcessing"
    >
      <span v-if="!isProcessing">Checkout (${{ totalPrice }})</span>
      <div v-else class="spinner-border" role="status">
        <span class="sr-only">Loading...</span>
      </div>
    </button>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  data() {
    return {
      orderPlace: false,
      isProcessing: false,
    };
  },
  computed: {
    ...mapGetters(["cart"]),
    totalPrice() {
      return this.cart.reduce((a, b) => a + b.qty * b.price, 0);
    },
  },
  methods: {
    ...mapActions(["addQty", "reduceQty", "removeItem", "emptyCart"]),
    PlaceOrder() {
      this.isProcessing = true;
      setTimeout(() => {
        this.orderPlace = true;
        this.isProcessing = false;
        this.emptyCart();
      }, 1000);
    },
  },
};
</script>>

<style scoped>
.btn-qty {
  border-radius: 50%;
  width: 30px;
}

.media {
  width: 90%;
}

.media-body {
  text-align: left;
}
</style>