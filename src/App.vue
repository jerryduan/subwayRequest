<template>
  <div id="app">
    <div class="container">
      <header>
        <h1>地铁乘客满意度调查</h1>
        <p class="subtitle">感谢您参与本次调查，您的反馈对我们非常重要</p>
      </header>

      <survey-form @submit-success="showSuccessModal"></survey-form>

      <!-- 提交成功弹窗 -->
      <success-modal 
        v-if="showModal" 
        @close="showModal = false"
      ></success-modal>
    </div>
  </div>
</template>

<script>
import SurveyForm from './components/survey/SurveyForm.vue'
import SuccessModal from './components/survey/SuccessModal.vue'

export default {
  name: 'App',
  components: {
    SurveyForm,
    SuccessModal
  },
  data() {
    return {
      showModal: false
    }
  },
  methods: {
    showSuccessModal() {
      this.showModal = true
    }
  }
}
</script>

<style>
/* 全局样式 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'PingFang SC', 'Helvetica Neue', Arial, sans-serif;
}

body {
  background-color: #f5f5f5;
  color: #333;
  line-height: 1.6;
}

#app {
  min-height: 100vh;
  background-color: #f5f5f5;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  min-height: 100vh;
}

/* 头部样式 */
header {
  text-align: center;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 1px solid #eee;
}

header h1 {
  color: #0078d7;
  font-size: 24px;
  margin-bottom: 10px;
}

.subtitle {
  color: #666;
  font-size: 14px;
}

/* 响应式调整 */
@media (max-width: 480px) {
  .container {
    padding: 15px;
  }
  
  header h1 {
    font-size: 22px;
  }
}
</style>
