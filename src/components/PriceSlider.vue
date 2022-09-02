<template>
  <transition
    name="custom"
    enter-active-class="animate__animated  animate__fadeInDown"
    leave-active-class="animate__animated  animate__slideOutRight"
  >
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label for="" class="form-label font-weight-bold mr-2">Max</label>
        <input
          type="number"
          class="form-control w-2"
          style="width: 200px; text-align: center"
          v-model="maxAmount"
          @change="$emit('update:maximum', maxAmount)"
        />
        <input
          type="range"
          name=""
          id=""
          class="form-range"
          min="0"
          max="200"
          v-model="maxAmount"
          @input="$emit('update:maximum', maxAmount)"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  props: ["maximum", "sliderStatus"],
  data: function () {
    return {
      maxAmount: 50,
    };
  },
  computed: {
    console: () => console,
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
</style>
