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
  margin-bottom: 28px;
  padding: 24px;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 
    0 8px 32px rgba(102, 126, 234, 0.1),
    0 2px 8px rgba(0, 0, 0, 0.05);
  position: relative;
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.question-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, #667eea, #764ba2);
  border-radius: 16px 16px 0 0;
}

.question-section:hover {
  transform: translateY(-2px);
  box-shadow: 
    0 12px 40px rgba(102, 126, 234, 0.15),
    0 4px 12px rgba(0, 0, 0, 0.1);
}

.question-section h2 {
  font-size: 19px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 20px;
  padding-bottom: 12px;
  font-weight: 600;
  position: relative;
  letter-spacing: 0.5px;
}

.question-section h2::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 30px;
  height: 2px;
  background: linear-gradient(90deg, #667eea, #764ba2);
  border-radius: 1px;
  opacity: 0.6;
}

@media (max-width: 480px) {
  .question-section {
    padding: 20px;
    margin-bottom: 24px;
    border-radius: 14px;
  }
  
  .question-section h2 {
    font-size: 17px;
    margin-bottom: 16px;
    padding-bottom: 10px;
  }
}

@media (max-width: 360px) {
  .question-section {
    padding: 16px;
    margin-bottom: 20px;
  }
  
  .question-section h2 {
    font-size: 16px;
  }
}
</style>