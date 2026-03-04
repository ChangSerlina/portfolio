<template>
  <div class="modal-overlay" v-if="isOpen" @click="closeModal">
    <div class="modal-content" @click.stop>
      <button class="close-btn" @click="closeModal">×</button>
      
      <h2>Schedule Free Consultation</h2>
      
      <form @submit.prevent="handleSubmit">
        <!-- 姓名 -->
        <div class="form-group">
          <label for="name">Name *</label>
          <input
            id="name"
            v-model="formData.name"
            type="text"
            placeholder="Please enter your name"
            required
          />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>

        <!-- 電話 -->
        <div class="form-group">
          <label for="phone">Phone *</label>
          <input
            id="phone"
            v-model="formData.phone"
            type="tel"
            placeholder="Please enter your phone number"
            required
          />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>

        <!-- 日期 -->
        <div class="form-group">
          <label for="date">Consultation Date *</label>
          <input
            id="date"
            v-model="formData.date"
            type="date"
            required
          />
          <span v-if="errors.date" class="error">{{ errors.date }}</span>
        </div>

        <!-- 諮詢簡述 -->
        <div class="form-group">
          <label for="description">Consultation Description *</label>
          <textarea
            id="description"
            v-model="formData.description"
            placeholder="Please describe your consultation needs"
            rows="4"
            required
          ></textarea>
          <span v-if="errors.description" class="error">{{ errors.description }}</span>
        </div>

        <!-- 提交按鈕 -->
        <div class="form-actions">
          <button type="button" class="btn-cancel" @click="closeModal">Cancel</button>
          <button 
            type="submit" 
            class="btn-submit"
            :disabled="isSubmitting"
          >
            {{ isSubmitting ? 'Submitting...' : 'Submit' }}
          </button>
        </div>

        <!-- 成功消息 -->
        <div v-if="successMessage" class="success-message">
          {{ successMessage }}
        </div>

        <!-- 錯誤消息 -->
        <div v-if="errorMessage" class="error-message">
          {{ errorMessage }}
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['close'])

const formData = ref({
  name: '',
  phone: '',
  date: '',
  description: ''
})

const errors = ref({})
const isSubmitting = ref(false)
const successMessage = ref('')
const errorMessage = ref('')

const closeModal = () => {
  emit('close')
  resetForm()
}

const resetForm = () => {
  formData.value = {
    name: '',
    phone: '',
    date: '',
    description: ''
  }
  errors.value = {}
  successMessage.value = ''
  errorMessage.value = ''
}

const validateForm = () => {
  errors.value = {}

  if (!formData.value.name.trim()) {
    errors.value.name = 'Name cannot be empty'
  }

  if (!formData.value.phone.trim()) {
    errors.value.phone = 'Phone cannot be empty'
  } else if (!/^[\d\-+\s()]+$/.test(formData.value.phone)) {
    errors.value.phone = 'Phone number format is incorrect'
  }

  if (!formData.value.date) {
    errors.value.date = 'Please select a consultation date'
  } else {
    const selectedDate = new Date(formData.value.date)
    const today = new Date()
    today.setHours(0, 0, 0, 0)
    if (selectedDate < today) {
      errors.value.date = 'Please select a future date'
    }
  }

  if (!formData.value.description.trim()) {
    errors.value.description = 'Consultation description cannot be empty'
  }

  return Object.keys(errors.value).length === 0
}

const handleSubmit = async () => {
  if (!validateForm()) {
    return
  }

  isSubmitting.value = true
  errorMessage.value = ''
  successMessage.value = ''

  try {
    // 替換為你的實際後端API端點
    const apiUrl = import.meta.env.VITE_API_URL || 'http://localhost:8000/api'
    
    // 準備數據，確保日期格式正確
    const submitData = {
      ...formData.value,
      date: formData.value.date // 確保發送 YYYY-MM-DD 格式
    }
    
    const response = await fetch(`${apiUrl}/consultations`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(submitData)
    })

    if (!response.ok) {
      throw new Error(`API error: ${response.status}`)
    }

    const data = await response.json()
    successMessage.value = 'Appointment successfully scheduled! We will contact you soon.'
    
    // 3秒後關閉模態框
    setTimeout(() => {
      closeModal()
    }, 3000)
  } catch (error) {
    console.error('Submission error:', error)
    errorMessage.value = 'Submission failed. Please check your network connection or try again later.'
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  border-radius: 8px;
  padding: 2rem;
  max-width: 500px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  position: relative;
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #666;
  width: 2rem;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.close-btn:hover {
  background-color: #f0f0f0;
  color: #000;
}

h2 {
  margin-top: 0;
  margin-bottom: 1.5rem;
  color: #333;
  text-align: center;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #333;
}

input,
textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-family: inherit;
  font-size: 1rem;
  transition: border-color 0.2s;
  box-sizing: border-box;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #4a90e2;
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.1);
}

textarea {
  resize: vertical;
  min-height: 100px;
}

.error {
  display: block;
  color: #e74c3c;
  font-size: 0.875rem;
  margin-top: 0.25rem;
}

.error-message {
  background-color: #ffe5e5;
  color: #c0392b;
  padding: 1rem;
  border-radius: 4px;
  margin-top: 1rem;
  border-left: 4px solid #e74c3c;
}

.success-message {
  background-color: #e8f8f5;
  color: #27ae60;
  padding: 1rem;
  border-radius: 4px;
  margin-top: 1rem;
  border-left: 4px solid #27ae60;
}

.form-actions {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

button {
  flex: 1;
  padding: 0.75rem;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.btn-cancel {
  background-color: #ecf0f1;
  color: #333;
}

.btn-cancel:hover {
  background-color: #d5dbdb;
}

.btn-submit {
  background-color: #4a90e2;
  color: white;
}

.btn-submit:hover:not(:disabled) {
  background-color: #357abd;
}

.btn-submit:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

@media (max-width: 768px) {
  .modal-content {
    width: 95%;
    padding: 1.5rem;
  }

  h2 {
    font-size: 1.25rem;
  }
}
</style>
