<script setup lang="ts">
import { defineProps, toRefs } from "vue";
import { IFormData } from "../models/IFormData";
import { IOption } from "../models/IOption";

interface DropdownProps {
  formData: IFormData;
  options: IOption[];
  error?: string;
  onBlur?: (id: string) => void;
}
const props = defineProps<DropdownProps>();
const { formData } = toRefs(props);
</script>

<template>
  <div>
    <label :for="props.options[0].name">Role:</label>
    <select
      :id="props.options[0].name"
      v-model="formData[props.options[0].name]"
      :name="props.options[0].name"
      @blur="props.onBlur ? props.onBlur(props.options[0].name) : null"
    >
      <option
        v-for="option in props.options"
        :key="option.id"
        :value="option.value"
      >
        {{ option.value }}
      </option>
    </select>
    <div v-if="props.error" class="error">{{ props.error }}</div>
  </div>
</template>

<style scoped></style>
