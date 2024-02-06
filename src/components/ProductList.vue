<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row d-none mb-0 align-items-center"
      v-for="(item, index) in showItem"
      :key="item.id"
      :data-index="index"
    >
      <div class="row d-flex mb-3 align-items-center">
        <div class="col-1 m-auto">
          <button class="btn btn-info" @click="$emit('add', item)">+</button>
        </div>
        <div class="col-sm-4">
          <img class="img-fluid d-block" :src="item.image" :alt="item.name" />
        </div>
        <div class="col">
          <h2 class="text-info">{{ item.name }}</h2>
          <p class="mb-0">{{ item.description }}</p>
          <div class="h5 float-right">
            <price :value="Number(item.price)"></price>
          </div>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";
export default {
  name: "product-list",
  component: {
    Price,
  },
  props: ["products", "maximum"],
  computed: {
    showItem: function () {
      let max = this.maximum;
      return this.products.filter(function (item) {
        return item.price <= max;
      });
    },
  },
  methods: {
    before: function (el) {
      el.className = "d-none";
    },
    enter: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-0 align-items-center animate__animated animate__fadeInLeft";
      }, delay);
    },
    leave: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-0 align-items-center animate__animated animate__fadeOutLeft";
      }, delay);
    },
  },
};
</script>
