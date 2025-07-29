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
.question {
  margin-bottom: 24px;
}

.question label:first-child {
  display: block;
  font-size: 16px;
  font-weight: 500;
  color: #4a5568;
  margin-bottom: 20px;
  line-height: 1.5;
}

.question label:first-child.error {
  color: #e53e3e;
}

.rating {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 8px;
  padding: 16px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 20px;
  border: 1px solid rgba(102, 126, 234, 0.1);
}

.rating-option {
  text-align: center;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.rating-option input[type="radio"] {
  display: none;
}

.rating-option label {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.9);
  border: 2px solid #e2e8f0;
  margin: 0 auto 8px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-weight: 600;
  font-size: 16px;
  color: #64748b;
  position: relative;
  overflow: hidden;
}

.rating-option label::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0);
  width: 20px;
  height: 20px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 50%;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  opacity: 0.2;
}

.rating-option label:hover {
  transform: translateY(-2px) scale(1.05);
  border-color: #667eea;
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.2);
}

.rating-option label:hover::before {
  transform: translate(-50%, -50%) scale(1);
}

.rating-option label.selected {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: #fff;
  border-color: #667eea;
  transform: translateY(-2px) scale(1.1);
  box-shadow: 
    0 8px 25px rgba(102, 126, 234, 0.3),
    0 0 0 3px rgba(102, 126, 234, 0.1);
}

.rating-option label.selected::before {
  display: none;
}

.rating-option span {
  display: block;
  font-size: 11px;
  color: #6b7280;
  font-weight: 500;
  text-align: center;
  line-height: 1.2;
  max-width: 60px;
  word-wrap: break-word;
}

.rating-option:first-child span,
.rating-option:last-child span {
  font-weight: 600;
  color: #4b5563;
}

@media (max-width: 480px) {
  .rating {
    padding: 12px 8px;
    gap: 4px;
  }
  
  .rating-option label {
    width: 42px;
    height: 42px;
    font-size: 14px;
    margin-bottom: 6px;
  }
  
  .rating-option label::before {
    width: 16px;
    height: 16px;
  }
  
  .rating-option span {
    font-size: 10px;
    max-width: 50px;
  }
  
  .question label:first-child {
    font-size: 15px;
    margin-bottom: 16px;
  }
}

@media (max-width: 360px) {
  .rating {
    padding: 10px 6px;
    gap: 2px;
  }
  
  .rating-option label {
    width: 36px;
    height: 36px;
    font-size: 13px;
  }
  
  .rating-option span {
    font-size: 9px;
    max-width: 45px;
  }
  
  .question label:first-child {
    font-size: 14px;
  }
}
</style>