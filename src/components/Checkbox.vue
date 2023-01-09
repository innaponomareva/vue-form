<script setup lang="ts">
import { defineProps, toRefs } from "vue";
import { IFormData } from "../models/IFormData";

interface CheckboxProps {
  id: string;
  label: string;
  name: string;
  formData: IFormData;
  error?: string;
  onBlur?: (id: string) => void;
}
const props = defineProps<CheckboxProps>();
const { formData } = toRefs(props);
</script>

<template>
  <div>
    <div>
      <input
        :id="props.id"
        v-model="formData[props.name]"
        type="checkbox"
        :value="props.label"
        @blur="props.onBlur ? props.onBlur(props.name) : null"
      />
      <label for="html">{{ props.label }}</label>
    </div>
    <div v-if="props.error" class="error">{{ props.error }}</div>
  </div>
</template>

<style scoped>
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
label {
  margin: 0;
}
</style>
