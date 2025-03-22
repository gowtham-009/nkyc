<template>
    <div>
      <FloatLabel variant="in">
        <InputText
          id="in_label"
          class="w-full"
          v-model="localPhoneNo"
          variant="filled"
          @keypress="allowOnlyNumbers"
        />
        <label for="in_label">Phone no*</label>
      </FloatLabel>
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const localPhoneNo = ref(props.modelValue || '');
  
  const allowOnlyNumbers = (e) => {
    if (!/^\d$/.test(e.key) || localPhoneNo.value.length >= 10) {
      e.preventDefault();
    }
  };
  
  // Watch for changes and emit the value
  watch(localPhoneNo, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  