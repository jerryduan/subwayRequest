<template>
  <div class="question">
    <label :for="name" :class="{ 'error': error }">{{ label }}</label>
    <div class="options">
      <label 
        v-for="option in options" 
        :key="option.value"
        class="radio-option"
        :class="{ 'selected': selectedValue === option.value }"
      >
        <input 
          type="radio" 
          :name="name" 
          :value="option.value"
          :required="required"
          v-model="selectedValue"
        >
        <span>{{ option.label }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RadioGroup',
  props: {
    label: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    options: {
      type: Array,
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
  margin-bottom: 16px;
  line-height: 1.5;
}

.question label:first-child.error {
  color: #e53e3e;
}

.options {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.radio-option {
  display: flex;
  align-items: center;
  padding: 12px 18px;
  background: rgba(255, 255, 255, 0.9);
  border: 2px solid rgba(102, 126, 234, 0.2);
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  font-size: 14px;
  font-weight: 500;
  color: #4a5568;
  min-height: 44px;
  box-sizing: border-box;
}

.radio-option::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.5s;
}

.radio-option:hover {
  border-color: #667eea;
  background: rgba(102, 126, 234, 0.05);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.15);
}

.radio-option:hover::before {
  left: 100%;
}

.radio-option input[type="radio"] {
  width: 18px;
  height: 18px;
  margin-right: 10px;
  position: relative;
  appearance: none;
  -webkit-appearance: none;
  border: 2px solid #d1d5db;
  border-radius: 50%;
  background: #fff;
  cursor: pointer;
  transition: all 0.3s;
}

.radio-option input[type="radio"]::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0);
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea, #764ba2);
  transition: transform 0.2s;
}

.radio-option input[type="radio"]:checked {
  border-color: #667eea;
  background: rgba(102, 126, 234, 0.1);
}

.radio-option input[type="radio"]:checked::before {
  transform: translate(-50%, -50%) scale(1);
}

.radio-option.selected {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1), rgba(118, 75, 162, 0.1));
  border-color: #667eea;
  color: #667eea;
  font-weight: 600;
}

.radio-option span {
  user-select: none;
}

@media (max-width: 480px) {
  .radio-option {
    padding: 10px 16px;
    font-size: 13px;
    min-height: 40px;
  }
  
  .radio-option input[type="radio"] {
    width: 16px;
    height: 16px;
    margin-right: 8px;
  }
  
  .radio-option input[type="radio"]::before {
    width: 6px;
    height: 6px;
  }
  
  .question label:first-child {
    font-size: 15px;
    margin-bottom: 14px;
  }
  
  .options {
    gap: 10px;
  }
}

@media (max-width: 360px) {
  .radio-option {
    padding: 8px 14px;
    font-size: 12px;
    min-height: 36px;
  }
  
  .question label:first-child {
    font-size: 14px;
  }
}
</style>