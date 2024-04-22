<template>
  <nav class="navbar navbar-light">
    <h1 class="fw-bold">EasyShop</h1>
    <div class="navbar-text ms-auto d-flex">
      <button
        class="btn btn-sm btn-outline-success"
        @click="$emit('toggle-slide')"
      >
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="ms-2 dropdown">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          type="button"
          id="dropdownCart"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <span class="me-2">|</span>
          <price :value="Number(cartTotal)"></price>
        </button>

        <div
          class="dropdown-menu dropdown-menu-sm dropdown-menu-end"
          aria-labelledby="dropdownCart"
        >
          <div v-if="cartTotal === 0" class="dropdown-item text-center">
            <i class="fa fa-trash text-success"></i>
            <span class="text-success fw-bold">Empty Cart</span>
          </div>
          <div v-else>
            <div v-for="(item, index) in cart" :key="index">
              <div class="dropdown-item-text text-nowrap text-start d-flex">
                <span
                  class="badge rounded-pill text-bg-success align-text-top me-1"
                >
                  {{ item.qty }}
                </span>
                {{ item.product.name }}
                <b class="ms-2 me-2">
                  {{ (item.qty * item.product.price) | currencyFormat }}</b
                >
                <button
                  class="btn btn-danger text-white btn-sm ms-auto"
                  @click.stop="$emit('delete-item', index)"
                >
                  -
                </button>
              </div>
            </div>
            <router-link
              class="btn btn-sm btn-success text-light fw-bold float-end mt-2 me-3"
              to="/checkout"
              active-class="hover-class"
              >Checkout</router-link
            >
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";

export default {
  name: "navbar",
  props: ["cart", "cartQty", "cartTotal"],
  components: {
    Price,
    FontAwesomeIcon,
  },
  filters: {
    currencyFormat: function (value) {
      return "$" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
