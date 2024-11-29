<template>
 <nav class="navbar navbar-light fixed-top">
  <div class="navbar-text ml-auto d-flex">
   <button class="btn btn-sm btn-outline-success" @click="$emit('toggle-slider')">
    <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
   </button>
   <div class="dropdown ml-2" v-if="cart.length > 0">
    <button class="btn btn-success btn-sm dropdown-toggle" id="dropdownCart" data-toggle="dropdown" aria-haspopup="true"
     aria-expanded="false">
     <span class="badge badge-fill badge-success">{{ cartQty }}</span>
     <font-awesome-icon icon="cart-shopping"></font-awesome-icon>
     <product-price :value="Number(cartTotal)" :precision="2" :prefix="'Rp'"></product-price>
    </button>
    <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownCart">
     <div v-for="(item, index) in cart" :key="index">
      <div class="dropdown-item-text text-nowrap text-right">
       <span class="badge badge-pill badge-warning align-text-top mr-1">
        {{ item.qty }}
       </span> {{ item.product.title }}
       <b>
        <product-price :value="Number(item.product.price * item.qty)" :precision="2" :prefix="'Rp'"></product-price>
       </b>
       <a href="#" class="badge badge-danger text-white" @click.stop="$emit('delete-item', index)">-</a>
      </div>
     </div>
     <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-2" to="/checkout">Checkout</router-link>
    </div>
   </div>
  </div>
 </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductPrice from "./ProductPrice.vue"
export default {
 name: "navbar",
 components: {
  ProductPrice,
  FontAwesomeIcon
 },
 props: ["cart", "cartQty", "cartTotal"],
 filters: {
  currencyFormat: function (value) {
   return "Rp" + Number.parseFloat(value).toFixed(2);
  },
 },
}
</script>