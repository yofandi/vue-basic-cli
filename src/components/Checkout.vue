<template>
  <div>
    <h1>Checkout</h1>
    <table class="table table-hover" v-if="cart.length">
      <caption class="text-right h3">
        <b>Total:</b>
        <price
          class="d-block text-success font-weight-light"
          :value="Number(cartTotal)"
        ></price>
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-center">Price</th>
          <th scope="col" class="text-center">Sub-Total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cart" :key="item.product.id">
          <td class="text-center">
            <div class="btn-group">
              <button
                @click="$emit('add', item.product)"
                type="button"
                class="btn btn-info"
              >
                +
              </button>
              <button
                @click="$emit('delete', index)"
                type="button"
                class="btn btn-outline-info"
              >
                -
              </button>
            </div>
          </td>
          <td scope="row">{{ item.product.name }}</td>
          <td class="text-center">{{ item.qty }}</td>
          <td class="text-right">
            <price :value="Number(item.product.price)"></price>
          </td>
          <td class="text-right">
            <price :value="Number(item.product.price * item.qty)"></price>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- eslint-disable-next-line-->
    <router-link class="btn btn-outline-info text-dark" to="/"
      >Back to Home</router-link
    >
  </div>
</template>

<script>
import Price from "./PricePages.vue";
export default {
  name: "MyCheckout",
  props: ["cart", "cartTotal"],
  components: {
    Price,
  },
};
</script>
