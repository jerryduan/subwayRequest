<template>
  <form @submit.prevent="submitForm">
    <!-- 基本信息 -->
    <section-container title="基本信息">
      <radio-group 
        label="您的性别："
        name="gender"
        :options="genderOptions"
        v-model="formData.gender"
        :required="true"
      ></radio-group>

      <radio-group 
        label="您的年龄段："
        name="age"
        :options="ageOptions"
        v-model="formData.age"
        :required="true"
      ></radio-group>

      <radio-group 
        label="您乘坐地铁的频率："
        name="frequency"
        :options="frequencyOptions"
        v-model="formData.frequency"
        :required="true"
      ></radio-group>
    </section-container>

    <!-- 满意度评价 -->
    <section-container title="满意度评价">
      <rating-group 
        label="您对地铁车厢内的清洁度满意吗？"
        name="cleanliness"
        v-model="formData.cleanliness"
        :required="true"
      ></rating-group>

      <rating-group 
        label="您对地铁运行的准点率满意吗？"
        name="punctuality"
        v-model="formData.punctuality"
        :required="true"
      ></rating-group>

      <rating-group 
        label="您对地铁站内的指示标识清晰度满意吗？"
        name="signage"
        v-model="formData.signage"
        :required="true"
      ></rating-group>

      <rating-group 
        label="您对地铁工作人员的服务态度满意吗？"
        name="service"
        v-model="formData.service"
        :required="true"
      ></rating-group>
    </section-container>

    <!-- 多选题 -->
    <section-container title="乘车体验">
      <checkbox-group 
        label="您认为地铁需要改进的方面有哪些？（可多选）"
        name="improvements"
        :options="improvementOptions"
        v-model="formData.improvements"
      ></checkbox-group>

      <div class="question" v-if="showOtherImprovements">
        <label for="otherImprovements">如选择"其他"，请说明：</label>
        <textarea 
          id="otherImprovements" 
          v-model="formData.otherImprovements" 
          rows="3"
        ></textarea>
      </div>
    </section-container>

    <!-- 开放性问题 -->
    <section-container title="建议与反馈">
      <div class="question">
        <label for="suggestions">您对地铁服务有什么建议或意见？</label>
        <textarea 
          id="suggestions" 
          v-model="formData.suggestions" 
          rows="5"
        ></textarea>
      </div>
    </section-container>

    <!-- 联系方式（选填） -->
    <section-container title="联系方式（选填）">
      <div class="question">
        <label for="phone">手机号码：</label>
        <input 
          type="tel" 
          id="phone" 
          v-model="formData.phone" 
          pattern="[0-9]{11}"
        >
        <small>用于后续调查或抽奖活动通知</small>
      </div>
    </section-container>

    <div class="submit-container">
      <button type="submit">提交问卷</button>
    </div>
  </form>
</template>

<script>
import SectionContainer from './SectionContainer.vue'
import RadioGroup from './RadioGroup.vue'
import RatingGroup from './RatingGroup.vue'
import CheckboxGroup from './CheckboxGroup.vue'

export default {
  name: 'SurveyForm',
  components: {
    SectionContainer,
    RadioGroup,
    RatingGroup,
    CheckboxGroup
  },
  data() {
    return {
      formData: {
        gender: '',
        age: '',
        frequency: '',
        cleanliness: '',
        punctuality: '',
        signage: '',
        service: '',
        improvements: [],
        otherImprovements: '',
        suggestions: '',
        phone: ''
      },
      genderOptions: [
        { value: 'male', label: '男' },
        { value: 'female', label: '女' }
      ],
      ageOptions: [
        { value: 'below18', label: '18岁以下' },
        { value: '18-25', label: '18-25岁' },
        { value: '26-35', label: '26-35岁' },
        { value: '36-45', label: '36-45岁' },
        { value: '46-60', label: '46-60岁' },
        { value: 'above60', label: '60岁以上' }
      ],
      frequencyOptions: [
        { value: 'daily', label: '每天' },
        { value: 'weekly', label: '每周数次' },
        { value: 'monthly', label: '每月数次' },
        { value: 'rarely', label: '很少乘坐' }
      ],
      improvementOptions: [
        { value: 'crowding', label: '车厢拥挤度' },
        { value: 'airCondition', label: '空调温度' },
        { value: 'noise', label: '噪音控制' },
        { value: 'wifi', label: '网络信号' },
        { value: 'facilities', label: '站内设施' },
        { value: 'security', label: '安全措施' },
        { value: 'other', label: '其他' }
      ]
    }
  },
  computed: {
    showOtherImprovements() {
      return this.formData.improvements.includes('other')
    },
    isFormValid() {
      // 检查必填项
      return (
        this.formData.gender &&
        this.formData.age &&
        this.formData.frequency &&
        this.formData.cleanliness &&
        this.formData.punctuality &&
        this.formData.signage &&
        this.formData.service
      )
    }
  },
  methods: {
    submitForm() {
      if (!this.isFormValid) {
        alert('请填写所有必填项')
        return
      }

      // 这里可以添加数据提交到服务器的代码
      console.log('提交的数据:', this.formData)
      
      // 触发提交成功事件
      this.$emit('submit-success')
      
      // 重置表单
      this.resetForm()
    },
    resetForm() {
      this.formData = {
        gender: '',
        age: '',
        frequency: '',
        cleanliness: '',
        punctuality: '',
        signage: '',
        service: '',
        improvements: [],
        otherImprovements: '',
        suggestions: '',
        phone: ''
      }
    }
  }
}
</script>

<style scoped>
/* 问题样式 */
.question {
  margin-bottom: 24px;
}

.question label {
  display: block;
  font-size: 16px;
  font-weight: 500;
  color: #4a5568;
  margin-bottom: 12px;
  line-height: 1.5;
}

.question small {
  display: block;
  color: #6b7280;
  font-size: 13px;
  margin-top: 8px;
  font-weight: 400;
  opacity: 0.8;
}

/* 文本输入框样式 */
input[type="text"],
input[type="tel"],
textarea {
  width: 100%;
  padding: 16px 18px;
  border: 2px solid rgba(102, 126, 234, 0.2);
  border-radius: 12px;
  font-size: 15px;
  font-family: inherit;
  background: rgba(255, 255, 255, 0.9);
  color: #374151;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(5px);
}

input[type="text"]:focus,
input[type="tel"]:focus,
textarea:focus {
  border-color: #667eea;
  outline: none;
  background: rgba(255, 255, 255, 0.95);
  box-shadow: 
    0 0 0 3px rgba(102, 126, 234, 0.1),
    0 4px 12px rgba(102, 126, 234, 0.15);
  transform: translateY(-1px);
}

input[type="text"]::placeholder,
input[type="tel"]::placeholder,
textarea::placeholder {
  color: #9ca3af;
  font-weight: 400;
}

textarea {
  resize: vertical;
  min-height: 120px;
  line-height: 1.6;
}

/* 提交按钮样式 */
.submit-container {
  text-align: center;
  margin-top: 40px;
  margin-bottom: 60px;
  padding: 0 20px;
}

button[type="submit"] {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 16px 40px;
  font-size: 17px;
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
  min-width: 160px;
}

button[type="submit"]:before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

button[type="submit"]:hover {
  transform: translateY(-2px);
  box-shadow: 
    0 12px 35px rgba(102, 126, 234, 0.4),
    0 5px 15px rgba(0, 0, 0, 0.1);
}

button[type="submit"]:hover:before {
  left: 100%;
}

button[type="submit"]:active {
  transform: translateY(0);
  box-shadow: 
    0 5px 15px rgba(102, 126, 234, 0.3),
    0 2px 5px rgba(0, 0, 0, 0.1);
}

@media (max-width: 480px) {
  input[type="text"],
  input[type="tel"],
  textarea {
    padding: 14px 16px;
    font-size: 14px;
    border-radius: 10px;
  }
  
  textarea {
    min-height: 100px;
  }
  
  .submit-container {
    margin-top: 32px;
    margin-bottom: 40px;
    padding: 0 15px;
  }
  
  button[type="submit"] {
    padding: 14px 32px;
    font-size: 16px;
    min-width: 140px;
  }
  
  .question label {
    font-size: 15px;
    margin-bottom: 10px;
  }
  
  .question small {
    font-size: 12px;
    margin-top: 6px;
  }
}

@media (max-width: 360px) {
  input[type="text"],
  input[type="tel"],
  textarea {
    padding: 12px 14px;
    font-size: 13px;
  }
  
  button[type="submit"] {
    padding: 12px 28px;
    font-size: 15px;
    min-width: 120px;
  }
  
  .question label {
    font-size: 14px;
  }
}
</style>