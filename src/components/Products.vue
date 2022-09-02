<template>
  <div>
    <h1>IDShop</h1>
    <MyNavbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle-slide="toggleSlider"
      @delete-item="deleteItem"
    ></MyNavbar>
    <!-- untuk mengonaktifkan eslint dipriceslider dengan menambahkan eslinter disable diatas priceslider -->
    <!-- eslint-disable-next-line-->
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider>
    <product-list
      :products="products"
      :maximum="maximum"
      @add-item="addItem"
    ></product-list>
  </div>
</template>

<script>
import MyNavbar from "./Navbar.vue";
import ProductList from "./ProductList.vue";
import PriceSlider from "./PriceSlider.vue";

export default {
  name: "MyProduct",
  props: [
    "products",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
    "slideState",
  ],
  components: {
    MyNavbar,
    ProductList,
    PriceSlider,
  },
  methods: {
    toggleSlider: function () {
      this.$emit("toggle");
    },
    addItem: function (item) {
      this.$emit("add", item);
    },
    deleteItem: function (index) {
      this.$emit("delete", index);
    },
  },
  watch: {
    prop() {
      if (this.maximum === undefined && this.maximum !== undefined) {
        console.log(this.prop);
      }
    },
  },
};
</script>
