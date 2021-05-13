<template>
  <div class="nav-bar"></div>

    <div class="cart-display">
      <div class="cart">Cart({{ cart.length }})</div>
      <button class="button" 
              v-on:click="clearCart">
              Clear Cart
      </button>
    </div>
      
    <ProductDisplay :premium="premium" @add-to-cart="updateCart" @rem-from-cart="remFromCart"></ProductDisplay> <!-- @ = listen for the event  -->
      
  <!-- <HelloWorld msg="Welcome to My Vue.js App"/> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import ProductDisplay from './components/ProductDisplay.vue'

export default {
  name: 'App',
  data: function() { // data option (as an anonymous func)
        return {
            cart: [],
            premium: true
        }
  },
  methods: {
    updateCart(id) {
      this.cart.push(id)
    },
    remFromCart(id) {
      const index = this.cart.indexOf(id)
      if (index > -1) this.cart.splice(index, 1)
    },
    clearCart() {
      this.cart = []
    }
  },
  components: {
    ProductDisplay
    // HelloWorld
  }
}
</script>

<style scoped lang="css">
  @import "./assets/styles.css"; 
</style>
