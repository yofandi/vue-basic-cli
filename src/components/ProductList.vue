<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row mb-3 align-items-center"
      v-for="(item, index) in ShowItem"
      :key="item.id"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info" v-on:click="$emit('add-item', item)">
          +
        </button>
      </div>
      <div class="col-sm-4">
        <img class="img-fluid" v-bind:src="item.image" v-bind:alt="item.name" />
      </div>
      <div class="col">
        <h2 class="text-info">{{ item.name }}</h2>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right">
          <price :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./PricePages.vue";

export default {
  name: "product-list",
  components: {
    Price,
  },
  props: ["products", "maximum"],
  computed: {
    ShowItem: function () {
      let max = this.maximum;
      return this.products.filter(function (item) {
        // return item.price <= max;
        return Math.trunc(item.price) <= max;
      });
    },
  },
  methods: {
    before: function (el) {
      // ketika even method dijalankan maka function dapat mengambil data yang ada dalam tag ketika aksi dijalankan
      el.className = "d-none";
    },
    enter: function (el) {
      var delay = el.dataset.index * 100;
      // dalam vue js, style dapat diatur dalam penulisan vue code itu sendiri
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated  animate__fadeInRight";
      }, delay);
    },
    leave: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated  animate__fadeOutRight";
      }, delay);
    },
  },
};
</script>
