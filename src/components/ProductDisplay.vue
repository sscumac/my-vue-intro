<template>

  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <a :href="url">
          <img :src="image" :class="{'out-of-stock-img': !inStock}"> <!-- v-bind directive dynamically binding attribute to expression-->
        </a>
      </div> 

      <div class="product-image">
        <h1>{{ title + showSale }}</h1>
        <p v-if="inStock > 10">Loads In Stock!</p>
        <p v-else-if="inStock <= 10 && inStock > 0">Almost sold out!</p>
        <p v-else>Out of Stock</p>

        <p>Shipping: {{ shipping }} </p>

        <ul>
          <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
        </ul>
        <ul>
          <li v-for="(size, index) in sizes" :key="index">{{ size }}</li>
        </ul>
        <ul>
          <li v-for="(variant, index) in variants"
             :key="index" 
             @mouseenter="updateVariant(index)"
             class="color-circle"
             :style="{ backgroundColor: variant.color }">
          </li>
        </ul>
        <!-- <p v-show="inStock">In Stock</p> adds display none if false (more performant) -->
        <button class="button" 
                :class="{ disabledButton: !inStock }" 
                :disabled="!inStock"
                @click="addToCart">
                Add to Cart
        </button>
        <button class="button" 
                v-on:click="remFromCart">
                Remove from Cart
        </button>
      </div>
    </div>
  </div>

</template>

<script>
import socks_green from '@/assets/images/socks_green.jpg'
import socks_blue from '@/assets/images/socks_blue.jpg'

export default {
  name: 'ProductDisplay',
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  data: function() { // data option (as an anonymous func)
        return {
            product: 'Socks',
            brand: "Super Socks",
            selectedVariant: 0,
            onSale: true,
            url: 'https://github.com/sscumac',
            details: ['50% cotton', '30% wool', '20% polyester'],
            sizes: [39, 40, 41, 42, 45],
            variants: [
              { id: 2234, color: 'green', image: socks_green, quantity: 50 },
              { id: 2235, color: 'blue', image: socks_blue, quantity: 0 }
            ]
        }
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].id); // emit the event
      // console.log(this.variants[this.selectedVariant].id)
    },
    remFromCart() {
      this.$emit('rem-from-cart', this.variants[this.selectedVariant].id); // emit the event
    },
    updateVariant(index) {
      this.selectedVariant = index
    }
  },
  computed: { // computed properties
    title() {
      return this.brand + ' ' + this.product
    },
    image() {
      return this.variants[this.selectedVariant].image
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity
    },
    showSale() {
      return this.onSale ? 'is on Sale' : ' '
    },
    shipping() {
      return this.premium ? 'free' : 2.99
    }
  }
}
</script>