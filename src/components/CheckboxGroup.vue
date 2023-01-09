<script setup lang="ts">
import { defineProps } from "vue";
import Checkbox from "./Checkbox.vue";
import { IFormData } from "../models/IFormData";
import { IOption } from "../models/IOption";

interface CheckboxGroupProps {
  formData: IFormData;
  options: IOption[];
  error: string;
  onBlur?: (id: string) => void;
}
const props = defineProps<CheckboxGroupProps>();
</script>

<template>
  <div>
    <label>{{ options[0].name }}:</label>
    <div class="checkbox-group">
      <Checkbox
        v-for="option in props.options"
        :id="option.id"
        :key="option.id"
        :name="option.name"
        :form-data="props.formData"
        :label="option.value"
        :on-blur="props.onBlur"
      />
    </div>
    <div v-if="props.error" class="error">{{ props.error }}</div>
  </div>
</template>

<style scoped>
.checkbox-group {
  column-count: 3;
}
</style>
