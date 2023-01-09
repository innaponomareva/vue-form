<script setup lang="ts">
import { reactive, watch, ref } from "vue";
import CheckboxGroup from "./CheckboxGroup.vue";
import Dropdown from "./Dropdown.vue";
import TextInput from "./TextInput.vue";
import Checkbox from "./Checkbox.vue";
import { skills } from "../lib/skills";
import { roles } from "../lib/roles";

const formData = reactive({
  email: "",
  password: "",
  role: "no role",
  skills: [],
  terms: false,
});

const errors = reactive({
  email: "",
  password: "",
  role: "",
  skills: "",
  terms: "",
});

const isAllDataPresent = ref(false);
const isAnyError = ref(false);

const handleSubmit = (e) => {
  e.preventDefault();
  console.log(formData);
  alert(JSON.stringify(formData));
};

const handleBlur = (id: string) => {
  if (id === "email") {
    errors.email =
      formData.email.length > 0
        ? formData.email.includes("@" && ".")
          ? ""
          : "Bad formated"
        : "This field is required";
  } else if (id === "password") {
    errors.password =
      formData.password.length > 0
        ? formData.password.length > 5
          ? ""
          : "Password must be at least 6 chars long"
        : "This field is required";
  } else if (id === "role") {
    errors.role = formData.role !== "no role" ? "" : "This field is required";
  } else if (id === "skills") {
    errors.skills =
      formData.skills.length > 0 ? "" : "Please provide at least one skill";
  } else if (id === "terms") {
    errors.terms = formData.terms
      ? ""
      : "You should accept terms and conditions before creating an account.";
  }
};

const checkIfAllDataPresent = () => {
  const valid =
    formData.email.length > 0 &&
    formData.password.length > 0 &&
    formData.role !== "no role" &&
    formData.skills.length > 0 &&
    formData.terms;
  return valid;
};
const checkIfAnyError = () => {
  return Object.values(errors).filter((error) => error !== "").length > 0;
};
watch([formData], () => {
  isAllDataPresent.value = checkIfAllDataPresent();
});
watch([errors], () => {
  isAnyError.value = checkIfAnyError();
});
</script>

<template>
  <form @submit="handleSubmit">
    <TextInput
      id="email"
      name="email"
      type="email"
      label="Email"
      :form-data="formData"
      :error="errors.email"
      :on-blur="handleBlur"
    />
    <TextInput
      id="password"
      name="password"
      type="password"
      label="Password"
      :form-data="formData"
      :error="errors.password"
      :on-blur="handleBlur"
    />
    <Dropdown
      :options="roles"
      :form-data="formData"
      :error="errors.role"
      :on-blur="handleBlur"
    />
    <CheckboxGroup
      :options="skills"
      :form-data="formData"
      :error="errors.skills"
      :on-blur="handleBlur"
    />
    <Checkbox
      id="terms"
      name="terms"
      label="Accept terms and conditions"
      :form-data="formData"
      :error="errors.terms"
      :on-blur="handleBlur"
    />
    <div>
      <button
        :disabled="!isAllDataPresent || isAnyError"
        :class="!isAllDataPresent || isAnyError ? 'disabled' : 'submit'"
      >
        Create an Account
      </button>
    </div>
  </form>
</template>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}
label {
  color: "#aaa";
  display: inline-block;
  margin: 0 0 10px;
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input:focus,
select:focus {
  outline: none;
}
button {
  border: 0;
  border-radius: 20px;
  padding: 10px 20px;
  margin: 20px 0 0;
  color: white;
  display: block;
  margin-left: auto;
}
.submit {
  background-color: #0b6dff;
  cursor: pointer;
}
.disabled {
  background-color: #dbdbdb;
  cursor: auto;
}
.error {
  margin-top: 10px;
  color: red;
  font-size: 0.8rem;
  line-height: 1rem;
}
</style>
