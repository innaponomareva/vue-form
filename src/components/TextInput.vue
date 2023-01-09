<script setup lang="ts">
import { defineProps, toRefs } from "vue";
import { IFormData } from "../models/IFormData";

interface TextInputProps {
  id: string;
  name: string;
  label: string;
  type: "text" | "email" | "password";
  formData: IFormData;
  error?: string;
  onBlur: (id: string) => void;
}
const props = defineProps<TextInputProps>();
const { formData } = toRefs(props);
</script>

<template>
  <div>
    <label :for="props.id">{{ props.label }}:</label>
    <input
      :id="props.id"
      v-model="formData[id]"
      :name="props.name"
      :type="props.type"
      @blur="props.onBlur(props.id)"
    />
    <div v-if="props.error" class="error">{{ props.error }}</div>
  </div>
</template>

<style scoped></style>
