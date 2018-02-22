<template>
  <div class="rating" :style="ratingStyle">
    <span class="rating__star" :class="{ 'rating__star--selected': isSelected(1) }" @click.stop="updateRating(1)">
      <span class="rating__star" :class="{ 'rating__star--selected': isSelected(2) }" @click.stop="updateRating(2)">
        <span class="rating__star" :class="{ 'rating__star--selected': isSelected(3) }" @click.stop="updateRating(3)">
          <span class="rating__star" :class="{ 'rating__star--selected': isSelected(4) }" @click.stop="updateRating(4)">
            <span class="rating__star" :class="{ 'rating__star--selected': isSelected(5) }" @click.stop="updateRating(5)">
            </span>
          </span>
        </span>
      </span>
    </span>
  </div>
</template>

<style scoped>
.rating {
  font-size: 2.5rem;
  cursor: pointer;
  padding-bottom: 0.2em;

  --selected-char: "★";
  --unselected-char: "☆";
}

.rating__star {
  display: inline-block;
  color: goldenrod;
}

.rating__star::before {
  content: var(--unselected-char);
  display: inline-block;
  margin-right: 0.1em;
  animation: scaledown 50ms linear forwards;
}

.rating__star--selected::before,
.rating__star:hover::before {
  content: var(--selected-char);
}

.rating__star:hover::before {
  animation: scaleup 50ms linear forwards;
}

.rating__star--selected:hover .rating__star--selected:not(:hover)::before {
  content: var(--unselected-char);
}

@keyframes scaleup {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.5);
  }
}

@keyframes scaledown {
  0% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}

</style>

<script>
export default {
  props: {
    'selectedChar': {
      type: String,
      default: '★',
    },
    'unselectedChar': {
      type: String,
      default: '☆'
    }
  },

  model: {
    prop: 'stars',
    event: 'ratingUpdate'
  },

  computed: {
    ratingStyle: function() {
      return {
        '--selected-char': `"${this.selectedChar}"`,
        '--unselected-char': `"${this.unselectedChar}"`
      }
    }
  },

  methods: {
    updateRating(newRating) {
      // if the star clicked is already selected, remove the rating
      if (newRating === this.stars) --this.stars;
      else this.stars = newRating;

      this.$emit('ratingUpdate', this.stars);
    },

    isSelected: function(index) {
      return index <= this.stars;
    }
  },

  data() {
    return {
      stars: 0,
    }
  }
}
</script>
