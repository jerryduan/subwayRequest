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
  font-family: 'PingFang SC', 'Helvetica Neue', 'Segoe UI', 'Microsoft YaHei', Arial, sans-serif;
}

body {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: #333;
  line-height: 1.6;
  min-height: 100vh;
}

#app {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  position: relative;
}

#app::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: 
    radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(255, 255, 255, 0.15) 0%, transparent 50%),
    radial-gradient(circle at 40% 40%, rgba(120, 119, 198, 0.2) 0%, transparent 50%);
  pointer-events: none;
  z-index: 0;
}

.container {
  max-width: 420px;
  margin: 0 auto;
  padding: 20px;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  min-height: calc(100vh - 40px);
  position: relative;
  z-index: 1;
  margin-top: 20px;
  margin-bottom: 20px;
}

/* 头部样式 */
header {
  text-align: center;
  margin-bottom: 35px;
  padding: 25px 0;
  position: relative;
}

header::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, #667eea, #764ba2);
  border-radius: 2px;
}

header h1 {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 26px;
  font-weight: 700;
  margin-bottom: 12px;
  letter-spacing: 1px;
}

.subtitle {
  color: #6c757d;
  font-size: 15px;
  font-weight: 400;
  opacity: 0.8;
}

/* 响应式调整 */
@media (max-width: 480px) {
  .container {
    padding: 15px;
    margin: 10px;
    min-height: calc(100vh - 20px);
    border-radius: 15px;
    max-width: calc(100% - 20px);
  }
  
  header {
    padding: 20px 0;
    margin-bottom: 25px;
  }
  
  header h1 {
    font-size: 22px;
  }
  
  .subtitle {
    font-size: 14px;
  }
}

@media (max-width: 360px) {
  .container {
    padding: 12px;
    margin: 5px;
    min-height: calc(100vh - 10px);
  }
  
  header h1 {
    font-size: 20px;
  }
}
</style>
