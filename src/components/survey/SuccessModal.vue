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
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background-color: #fff;
  padding: 30px;
  border-radius: 15px;
  text-align: center;
  max-width: 80%;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.modal-content h2 {
  color: #0078d7;
  margin-bottom: 15px;
}

.modal-content p {
  margin-bottom: 10px;
  color: #555;
}

.modal-content button {
  background-color: #0078d7;
  color: white;
  border: none;
  padding: 10px 25px;
  font-size: 15px;
  border-radius: 20px;
  cursor: pointer;
  margin-top: 15px;
  transition: background-color 0.3s;
}

.modal-content button:hover {
  background-color: #0063b1;
}
</style>