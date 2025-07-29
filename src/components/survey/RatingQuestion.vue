<template>
  <div class="question">
    <label>{{ question }}</label>
    <div class="rating">
      <div 
        v-for="rating in 5" 
        :key="rating"
        class="rating-option"
      >
        <input 
          type="radio" 
          :id="`${fieldName}_${rating}`"
          :value="rating" 
          v-model="selectedValue"
          :required="required"
        >
        <label 
          :for="`${fieldName}_${rating}`"
          :class="{ active: selectedValue >= rating }"
        >
          {{ rating }}
        </label>
        <span v-if="rating === 1">非常不满意</span>
        <span v-if="rating === 5">非常满意</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RatingQuestion',
  props: {
    value: {
      type: [String, Number],
      default: ''
    },
    question: {
      type: String,
      required: true
    },
    required: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    selectedValue: {
      get() {
        return this.value
      },
      set(value) {
        this.$emit('input', value)
      }
    },
    fieldName() {
      return this.question.replace(/[^a-zA-Z0-9]/g, '_').toLowerCase()
    }
  }
}
</script>

<style scoped>
.question {
  margin-bottom: 20px;
}

.question label {
  display: block;
  margin-bottom: 10px;
  font-weight: 500;
  color: #444;
}

/* 评分样式 */
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
  font-weight: bold;
}

.rating-option input[type="radio"]:checked + label,
.rating-option label.active {
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

/* 响应式调整 */
@media (max-width: 480px) {
  .rating-option label {
    width: 35px;
    height: 35px;
    line-height: 35px;
  }
}
</style>