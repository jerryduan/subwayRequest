<template>
  <div class="modal">
    <div class="modal-content">
      <h2>提交成功</h2>
      <p>感谢您参与本次调查！</p>
      <p>您的反馈对我们改进地铁服务非常重要。</p>
      <button @click="closeModal">确定</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SuccessModal',
  methods: {
    closeModal() {
      this.$emit('close')
    }
  }
}
</script>

<style scoped>
.modal {
  display: flex;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(8px);
  z-index: 1000;
  align-items: center;
  justify-content: center;
  padding: 20px;
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideIn {
  from {
    transform: translate(-50%, -50%) scale(0.8);
    opacity: 0;
  }
  to {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
}

.modal-content {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  padding: 40px 35px;
  border-radius: 24px;
  text-align: center;
  max-width: 360px;
  width: 100%;
  box-shadow: 
    0 20px 50px rgba(102, 126, 234, 0.3),
    0 8px 25px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  position: relative;
  animation: slideIn 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.modal-content::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(90deg, #667eea, #764ba2);
  border-radius: 24px 24px 0 0;
}

.modal-content h2 {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 24px;
  font-weight: 700;
  margin-bottom: 20px;
  letter-spacing: 0.5px;
}

.modal-content p {
  margin-bottom: 12px;
  color: #4a5568;
  font-size: 16px;
  line-height: 1.6;
  font-weight: 400;
}

.modal-content p:last-of-type {
  margin-bottom: 30px;
  font-weight: 500;
  color: #667eea;
}

.modal-content button {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 14px 32px;
  font-size: 16px;
  font-weight: 600;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 
    0 8px 25px rgba(102, 126, 234, 0.3),
    0 3px 10px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
  letter-spacing: 0.5px;
  min-width: 120px;
}

.modal-content button:before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.modal-content button:hover {
  transform: translateY(-2px);
  box-shadow: 
    0 12px 35px rgba(102, 126, 234, 0.4),
    0 5px 15px rgba(0, 0, 0, 0.1);
}

.modal-content button:hover:before {
  left: 100%;
}

.modal-content button:active {
  transform: translateY(0);
  box-shadow: 
    0 5px 15px rgba(102, 126, 234, 0.3),
    0 2px 5px rgba(0, 0, 0, 0.1);
}

@media (max-width: 480px) {
  .modal {
    padding: 15px;
  }
  
  .modal-content {
    padding: 32px 28px;
    max-width: 320px;
    border-radius: 20px;
  }
  
  .modal-content h2 {
    font-size: 22px;
    margin-bottom: 16px;
  }
  
  .modal-content p {
    font-size: 15px;
    margin-bottom: 10px;
  }
  
  .modal-content p:last-of-type {
    margin-bottom: 24px;
  }
  
  .modal-content button {
    padding: 12px 28px;
    font-size: 15px;
    min-width: 100px;
  }
}

@media (max-width: 360px) {
  .modal-content {
    padding: 28px 24px;
    max-width: 280px;
  }
  
  .modal-content h2 {
    font-size: 20px;
  }
  
  .modal-content p {
    font-size: 14px;
  }
  
  .modal-content button {
    padding: 10px 24px;
    font-size: 14px;
  }
}
</style>