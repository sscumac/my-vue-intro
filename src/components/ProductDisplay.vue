<template>

  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <a :href="url">
          <img v-bind:src="image" :class="{'out-of-stock-img': !inStock}"> <!-- v-bind directive dynamically binding one way binding from data to template -->
        </a>
      </div> 

      <div class="product-image">
        <h1>{{ title + showSale }}</h1>
        <p v-if="inStock > 10">Loads In Stock!</p>
        <p v-else-if="inStock <= 10 && inStock > 0">Almost sold out!</p>
        <p v-else>Out of Stock</p>

        <p>Shipping: {{ shipping }} </p>

        <span>made of: </span>
        <span v-for="(detail, index) in details" :key="index">{{ showDetail(detail, index) }}</span>

        <br>

        <span>available sizes: </span>
        <span v-for="(size, index) in sizes" :key="index">{{ size + ' ' }}</span>

        <br>
       
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
    <ReviewList v-if="reviews.length" :reviews="reviews"></ReviewList> 
    <ReviewForm @review-submitted="addReview"></ReviewForm> 
  </div>

</template>

<script>
import socks_green from '@/assets/images/socks_green.jpg'
import socks_blue from '@/assets/images/socks_blue.jpg'
import ReviewForm from './ReviewForm.vue'
import ReviewList from './ReviewList.vue'

export default {
  name: 'ProductDisplay',
  components: {
    ReviewForm,
    ReviewList
  },
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
            ],
            reviews: []
        }
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].id); // emit the event
    },
    remFromCart() {
      this.$emit('rem-from-cart', this.variants[this.selectedVariant].id); // emit the event
    },
    updateVariant(index) {
      this.selectedVariant = index
    },
    addReview(review) { // review from the event payload
      this.reviews.push(review)
    },
     showDetail(detail, index) {
      return index < this.details.length - 1 ? `${detail}, ` : `${detail}` ;
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
      return this.onSale ? ' (on Sale)' : ' '
    },
    shipping() {
      return this.premium ? 'free' : 2.99
    }
  }
}
</script>