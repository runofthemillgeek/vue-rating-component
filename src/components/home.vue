<template>
  <div class="container">
    <div class="row mt-5">
      <div class="col-12">
        <h1 class="heading">Rating Component</h1>
        <img src="../assets/logo.png" alt="test">
      </div>
      <div class="col-12 mt-3">
        <form>
          <div class="form-group row">
            <label for="nameInput" class="col-form-label col-form-label-lg col-2">Name:</label>
            <div class="col-10">
              <input type="text" v-model="name" class="form-control form-control-lg">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-form-label-rating col-form-label col-form-label-lg col-2">Rating:</label>
            <div class="col-10">
              <app-rating v-model="rating" unselected-char="🖤" selected-char="💖" />
            </div>
          </div>
        </form>
        <p v-if="name.length > 0">{{ (name) | propercase }} gave a rating of {{ rating }} stars!</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .heading {
    color: indianred;
  }

  .col-form-label-rating {
    padding-top: 1em;
  }

  p {
    font-size: 3rem;
  }
</style>

<script>
import RatingComponent from './rating';

export default {
  components: {
    'app-rating': RatingComponent
  },

  data() {
    return {
      name: '',
      rating: 0,
    }
  },

  filters: {
    propercase: function(text) {
      return text.split(/\s+/).map(token => token[0] ? `${token[0].toUpperCase()}${token.slice(1)}` : '').join(' ');
    }
  }
}
</script>
