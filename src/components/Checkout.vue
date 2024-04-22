<template>
  <div>
    <h1>Checkout</h1>
    <div v-if="cart.length === 0">
      <h2 class="mt-3 mb-3 text-success-emphasis" style="opacity: 0.5">
        Your Checkout is empty
      </h2>
    </div>
    <table class="table table-hover" v-if="cart.length">
      <caption class="text-end h3">
        <b>Total : </b>
        <price
          class="d-block text-success fw-light"
          :value="Number(cartTotal)"
        ></price>
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col"></th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-end">Price</th>
          <th scope="col" class="text-end">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cart" :key="item.product.id">
          <td class="tex-center">
            <div class="btn-group">
              <button
                @click="$emit('add', item.product)"
                class="btn btn-success"
              >
                +
              </button>
              <button
                @click="$emit('delete', index)"
                class="btn btn-outline-success"
              >
                -
              </button>
            </div>
          </td>
          <th scope="row">{{ item.product.name }}</th>
          <th class="text-center">{{ item.qty }}</th>
          <th class="text-end">{{ Number(item.product.price).toFixed(2) }}</th>
          <th class="text-end">
            {{ Number(item.qty * item.product.price).toFixed(2) }}
          </th>
        </tr>
      </tbody>
    </table>
    <router-link class="btn btn-sm btn-success text-light fw-bold" to="/"
      >Back to Shop</router-link
    >
  </div>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "checkout",
  props: ["cart", "cartTotal"],
  components: {
    Price,
  },
};
</script>
