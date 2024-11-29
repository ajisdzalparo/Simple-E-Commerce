<template>
 <div>
  <transition-group name="fade" tag="div" @before-enter="before" @enter="enter" @leave="leave"
   enter-active-class="animate__animated animate__fadeInRight"
   leave-active-class="animate__animated animate__fadeOutRight">
   <div class="row mb-3 align-items-center" v-for="(item, index) in showItem" :key="index" v-bind:data-index="index">
    <div class="col-1 m-auto">
     <button class="btn btn-info" @click="$emit('add-item', item)">+</button>
    </div>
    <div class="col-sm-3 m-auto">
     <img :src="item.image" :alt="name" class="img-fluid">
    </div>
    <div class="col">
     <h3 class="text-info">{{ item.title }}</h3>
     <p class="mb-0">{{ item.description }}</p>
     <div class="h5 float-right">
      <product-price :value="Number(item.price)"></product-price>
     </div>
    </div>
   </div>
  </transition-group>
 </div>
</template>

<script>
import ProductPrice from "./ProductPrice.vue";

export default {
 name: "product-list",
 components: {
  ProductPrice,
 },
 data: function () {
  return {
   name: '',
  }
 },
 props: ["products", "maximum"],
 computed: {
  showItem: function () {
   let max = this.maximum;
   return this.products.filter(function (item) {
    return Math.trunc(item.price) <= max;
   })
  }
 },
 methods: {
  before: function (el) {
   el.class = "d-none";
  },
  enter: function (el) {
   var delay = el.dataset.index * 100;
   setTimeout(() => {
    el.className = "row d-flex mb-3 align-items-center animate__animated animate__fadeInRight";
   }, delay);
  },
  leave: function () {
   var delay = el.dataset.index * 100;
   setTimeout(() => {
    el.className = "row d-flex mb-3 align-items-center animate__animated animate__fadeOutRight";
   }, delay);
  },
 },
}
</script>