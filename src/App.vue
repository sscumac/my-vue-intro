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
            url: 'https://github.com/sscumac'
            // <img alt="Vue logo" src="./assets/logo.png">
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
