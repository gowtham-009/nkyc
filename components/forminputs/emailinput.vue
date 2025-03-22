<template>
    <div>
      <FloatLabel variant="in">
        <InputText
          id="in_label"
          class="w-full"
          v-model="email"
          variant="filled"
          @blur="validateEmail"
          size="large"
        />
        <label for="in_label">Email ID*</label>
      </FloatLabel>
      <p v-if="emailError" class="text-red-500">{{ emailError }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';

  const emailError = ref('');
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const email = ref(props.modelValue || '');

  const validateEmail = () => {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailPattern.test(email.value)) {
      emailError.value = 'Please enter a valid email address';
    } else {
      emailError.value = '';
    }
  };

  watch(email, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  
  <style>
  .text-red-500 {
    color: #ef4444; /* Tailwind error color */
  }
  </style>
  