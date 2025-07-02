<template>
  <div class="question">
    <label :class="{ 'error': error }">{{ label }}</label>
    <div class="rating">
      <div 
        v-for="n in 5" 
        :key="n"
        class="rating-option"
      >
        <input 
          type="radio" 
          :name="name" 
          :value="n.toString()" 
          :id="`${name}${n}`"
          :required="required"
          v-model="selectedValue"
        >
        <label 
          :for="`${name}${n}`"
          :class="{ 'selected': parseInt(selectedValue) >= n }"
        >{{ n }}</label>
        <span v-if="n === 1">非常不满意</span>
        <span v-if="n === 5">非常满意</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RatingGroup',
  props: {
    label: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    value: {
      type: String,
      default: ''
    },
    required: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      error: false
    }
  },
  computed: {
    selectedValue: {
      get() {
        return this.value
      },
      set(value) {
        this.$emit('input', value)
        this.error = false
      }
    }
  },
  methods: {
    validate() {
      if (this.required && !this.selectedValue) {
        this.error = true
        return false
      }
      return true
    }
  }
}
</script>

<style scoped>
.rating {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.rating-option {
  text-align: center;
  flex: 1;
}

.rating-option input[type="radio"] {
  display: none;
}

.rating-option label {
  display: block;
  width: 40px;
  height: 40px;
  line-height: 40px;
  border-radius: 50%;
  background-color: #fff;
  border: 1px solid #ddd;
  margin: 0 auto;
  cursor: pointer;
  transition: all 0.3s;
}

.rating-option label.selected {
  background-color: #0078d7;
  color: #fff;
  border-color: #0078d7;
}

.rating-option span {
  display: block;
  font-size: 12px;
  color: #666;
  margin-top: 5px;
}

.error {
  color: #e74c3c;
}

@media (max-width: 480px) {
  .rating-option label {
    width: 35px;
    height: 35px;
    line-height: 35px;
  }
}
</style>