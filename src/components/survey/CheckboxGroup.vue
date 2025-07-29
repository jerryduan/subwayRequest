<template>
  <div class="question">
    <label>{{ label }}</label>
    <div class="checkbox-options">
      <label 
        v-for="option in options" 
        :key="option.value"
        class="checkbox-option"
        :class="{ 'selected': selectedValues.includes(option.value) }"
      >
        <input 
          type="checkbox" 
          :name="name" 
          :value="option.value"
          v-model="selectedValues"
        >
        <span>{{ option.label }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CheckboxGroup',
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
      type: Array,
      default: () => []
    }
  },
  computed: {
    selectedValues: {
      get() {
        return this.value
      },
      set(value) {
        this.$emit('input', value)
      }
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

.checkbox-options {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.checkbox-option {
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

.checkbox-option::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.5s;
}

.checkbox-option:hover {
  border-color: #667eea;
  background: rgba(102, 126, 234, 0.05);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.15);
}

.checkbox-option:hover::before {
  left: 100%;
}

.checkbox-option input[type="checkbox"] {
  width: 18px;
  height: 18px;
  margin-right: 10px;
  position: relative;
  appearance: none;
  -webkit-appearance: none;
  border: 2px solid #d1d5db;
  border-radius: 4px;
  background: #fff;
  cursor: pointer;
  transition: all 0.3s;
}

.checkbox-option input[type="checkbox"]::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0) rotate(45deg);
  width: 6px;
  height: 10px;
  border: solid #fff;
  border-width: 0 2px 2px 0;
  transition: all 0.2s;
}

.checkbox-option input[type="checkbox"]:checked {
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-color: #667eea;
}

.checkbox-option input[type="checkbox"]:checked::before {
  transform: translate(-50%, -60%) scale(1) rotate(45deg);
}

.checkbox-option.selected {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1), rgba(118, 75, 162, 0.1));
  border-color: #667eea;
  color: #667eea;
  font-weight: 600;
}

.checkbox-option span {
  user-select: none;
}

@media (max-width: 480px) {
  .checkbox-option {
    padding: 10px 16px;
    font-size: 13px;
    min-height: 40px;
  }
  
  .checkbox-option input[type="checkbox"] {
    width: 16px;
    height: 16px;
    margin-right: 8px;
  }
  
  .checkbox-option input[type="checkbox"]::before {
    width: 5px;
    height: 8px;
  }
  
  .question label:first-child {
    font-size: 15px;
    margin-bottom: 14px;
  }
  
  .checkbox-options {
    gap: 10px;
  }
}

@media (max-width: 360px) {
  .checkbox-option {
    padding: 8px 14px;
    font-size: 12px;
    min-height: 36px;
  }
  
  .question label:first-child {
    font-size: 14px;
  }
}
</style>