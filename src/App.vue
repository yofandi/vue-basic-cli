<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App, bruhhh"/> -->

    <!-- saya komen karena ditutor 2 tag ini dipindah ke Product.vue -->
    <!-- <h1>IDShop</h1> -->
    <!-- <MyNavbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle="toggleSliderStatus" @delete="deleteItem"></MyNavbar> -->

    <!-- <p class="animate__animated animate__fadeInRight"> 
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
      quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
      consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
      cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
      proident, sunt in culpa qui officia deserunt mollit anim id est laborum. 
    </p>

    <font-awesome-icon icon="shopping-cart" />

    <price :value="4.32"></price> -->

    <!-- saya komen karena ditutor 2 tag ini dipindah ke Product.vue -->
    <!-- <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider> -->

    <!-- <product-list :products="products" :maximum="maximum" @add="addItem"></product-list> -->

    <!-- tag hanya digunakan ketika import components dilakukan -->
    <!-- <MyCheckout
      :cart="cart"
      :cartTotal="cartTotal"
      @add="addItem"
      @delete="deleteItem"
    ></MyCheckout>

    <MyProduct
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      :maximum.sync="maximum"
      :products="products"
      :sliderStatus="sliderStatus"
      @toggle="toggleSliderStatus"
      @add="addItem"
      @delete="deleteItem"
    ></MyProduct> -->

    <!-- dalam menggunakan VueRouter tidak lagi mencantumkan nama tag dari components, namun menulisnya dengan router-view. maka dengan otomatis ia akan mencari components berdasarkan router dan pathnya -->
    <router-view
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      :maximum.sync="maximum"
      :products="products"
      :sliderStatus="sliderStatus"
      @toggle="toggleSliderStatus"
      @add="addItem"
      @delete="deleteItem"
    ></router-view>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome"
// import Price from "./components/PricePages.vue"

// saya komen karena ditutor 3 import ini dipindah ke Product.vue
// import MyNavbar from "./components/Navbar.vue"
// import ProductList from "./components/ProductList.vue"
// import PriceSlider from "./components/PriceSlider.vue"

// ketika membuat router dengan VueRouter maka import dibawah dipindah ke main.js dan selanjutnya components dihapus
// import MyCheckout from "./components/Checkout.vue";
// import MyProduct from "./components/Products.vue";

export default {
  name: "App",
  data: function () {
    return {
      maximum: 50,
      products: [],
      cart: [],
      sliderStatus: false,
    };
  },
  // components: {
  // HelloWorld,
  // FontAwesomeIcon,
  // Price,
  // ProductList,
  // PriceSlider,
  // MyNavbar,

  // MyProduct,
  // MyCheckout,
  // },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  computed: {
    // membuat total rupiah keranjang
    cartTotal: function () {
      let sum = 0;
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    // membuat total jumal keranjang
    cartQty: function () {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    },
  },
  methods: {
    toggleSliderStatus: function () {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function (product) {
      let productIndex;
      let productExist = this.cart.filter(function (item, index) {
        if (item.product.id == Number(product.id)) {
          productIndex = index;
          return true;
        } else {
          return false;
        }
      });

      // untuk menampilkan qty dan product
      if (productExist.length) {
        this.cart[productIndex].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },

    // delete item product keranjang
    deleteItem: function (key) {
      if (this.cart[key].qty > 1) {
        this.cart[key].qty--;
      } else {
        this.cart.splice(key, 1);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
