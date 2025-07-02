<template>
  <div class="question">
    <label>{{ label }}</label>
    <div class="checkbox-options">
      <label 
        v-for="option in options" 
        :key="option.value"
        class="checkbox-option"
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
.checkbox-options {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 10px;
}

.checkbox-option {
  display: flex;
  align-items: center;
  padding: 8px 15px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s;
}

.checkbox-option:hover {
  border-color: #0078d7;
}

.checkbox-option input[type="checkbox"] {
  margin-right: 5px;
}

@media (max-width: 480px) {
  .checkbox-option {
    padding: 6px 12px;
  }
}
</style>