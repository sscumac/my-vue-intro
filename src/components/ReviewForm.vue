<template>

  <form class="review-form" @submit.prevent="onSubmit"> <!-- .prevent: modifier to prevent default -->
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="name"> <!-- v-model: two-way binding between input and data -->

    <label for="review">Review:</label>
    <textarea id="review" v-model="review"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating"> <!-- .number: modifier to typecast as a number -->
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <br>

    <label for="recommend">Would you recommend this product?</label>
    <select id="recommend" v-model.number="recommend">
      <option>yes</option>
      <option>no</option>
    </select>

    <input type="submit" class="button" value="Submit">

  </form>

</template>

<script>

export default {
  name: 'ReviewForm',
  data() {
    return {
      name: '',
      review: '',
      recommend: '',
      rating: null
    }
  },
  methods: {
    onSubmit() {
      if (this.name === "" || this.rating === "" || this.review === "" || this.recommend === "") {
        alert("Review incomplete")
        return // return out of the method
      } 
      let productReview = {
        name: this.name,
        review: this.review,
        recommend: this.recommend,
        rating: this.rating
      }
      this.$emit("review-submitted", productReview) // this.$emit(eventName, payload)

      // clear this shit out
      this.name = "",
      this.review = "",
      this.recommend = "",
      this.rating = null
    }
  }
}
</script>
