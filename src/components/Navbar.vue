<template>
  <nav class="navbar navbar-default bg-default fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button
        class="btn btn-sm btn-outline-success"
        @click="$emit('toggle-slide')"
      >
        <!-- <i class="fa-solid fa-dollar-sign"></i> -->
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>

      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button
          class="btn btn-sm btn-success dropdown-toggle"
          id="dropdownCart"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge rounded-pill text-bg-success">
            {{ cartQty }}
          </span>
          <!-- <i class="fa-solid fa-shopping-cart mx-2"></i> -->
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <!-- {{ cartTotal | currencyFormat }} -->
          <price :value="Number(cartTotal)"></price>
        </button>
        <div
          class="dropdown-menu dropdown-menu-right"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text textnowrap text-right">
              <span
                class="badge rounded-pill text-bg-warning align-text-top mr-1"
              >
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b> {{ (item.product.price * item.qty) | currencyFormat }} </b>
              <a
                href="#"
                class="badge rounded-pill text-bg-danger text-white"
                @click.stop="$emit('delete-item', index)"
              >
                -
              </a>
            </div>
          </div>

          <!-- eslint-disable-next-line-->
          <router-link
            class="btn btn-outline-info text-dark mr-2"
            to="/checkout"
            >Checkout</router-link
          >
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Price from "./PricePages.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "MyNavbar",
  components: {
    Price,
    FontAwesomeIcon,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp. " + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
