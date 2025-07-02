<template>
  <div class="question">
    <label :for="name" :class="{ 'error': error }">{{ label }}</label>
    <div class="options">
      <label 
        v-for="option in options" 
        :key="option.value"
        class="radio-option"
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
.options {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.radio-option {
  display: flex;
  align-items: center;
  padding: 8px 15px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s;
}

.radio-option:hover {
  border-color: #0078d7;
}

.radio-option input[type="radio"] {
  margin-right: 5px;
}

.error {
  color: #e74c3c;
}

@media (max-width: 480px) {
  .radio-option {
    padding: 6px 12px;
  }
}
</style>