<template>
  <div class="nav-bar"></div>
      
      <div class="product-display">
        <div class="product-container">
          <div class="product-image">
            <a :href="url">
              <img :src="image"> <!-- v-bind directive dynamically binding attribute to expression-->
            </a>
          </div> 
          <div class="product-image">
            <h1>{{ product }}</h1>
            <p v-if="inventory > 10">Loads In Stock!</p>
            <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
            <p v-else>Out of Stock</p>
            <p v-if="onSale">On Sale</p>
            <ul>
              <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
            </ul>
            <ul>
              <li v-for="(size, index) in sizes" :key="index">{{ size }}</li>
            </ul>
            <!-- <p v-show="inStock">In Stock</p> adds display none if false (more performant) -->
          </div>
        </div>
      </div>
  <!-- <HelloWorld msg="Welcome to My Vue.js App"/> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import socks_green from '@/assets/images/socks_green.jpg'

export default {
  name: 'App',
  data: function() { // data option
        return {
            product: 'Socks',
            image: socks_green,
            url: 'https://github.com/sscumac',
            inventory: 0,
            onSale: false,
            details: ['50% cotton', '30% wool', '20% polyester'],
            sizes: [39, 40, 41, 42, 45]
        }
  },
  components: {
    // HelloWorld
  }
}
</script>

<style scoped lang="css">
  @import "./assets/styles.css"; 
</style>
