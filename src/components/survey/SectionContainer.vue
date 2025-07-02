<template>
  <section class="question-section">
    <h2>{{ title }}</h2>
    <slot></slot>
  </section>
</template>

<script>
export default {
  name: 'SectionContainer',
  props: {
    title: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
.question-section {
  margin-bottom: 30px;
  padding: 15px;
  border-radius: 10px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
}

.question-section h2 {
  font-size: 18px;
  color: #0078d7;
  margin-bottom: 15px;
  padding-bottom: 8px;
  border-bottom: 1px solid #eee;
}

@media (max-width: 480px) {
  .question-section {
    padding: 12px;
  }
}
</style>