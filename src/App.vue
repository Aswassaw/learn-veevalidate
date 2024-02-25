<script setup lang="ts">
import * as yup from "yup";
import { useForm, useField } from "vee-validate";

type FormData = {
  name: string;
  email: string;
};

const { handleSubmit, errors } = useForm<FormData>({
  initialValues: {
    name: "",
    email: "",
  },
});
const { value: name } = useField("name", yup.string().required());
const { value: email } = useField("email", yup.string().email().required());

const submitForm = handleSubmit((values) => {
  console.log("Form submitted with values:", values);
});
</script>

<template>
  <div>
    <h1>Coba Vee Validate + Yup</h1>
    <form @submit.prevent="submitForm">
      <div style="margin-bottom: 10px">
        <label for="name"><span style="color: red">*</span> Name</label>
        <br />
        <input
          type="text"
          name="name"
          id="name"
          placeholder="Input Name"
          v-model="name"
        />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>
      </div>
      <div style="margin-bottom: 10px">
        <label for="email"><span style="color: red">*</span> Email</label>
        <br />
        <input
          type="email"
          name="email"
          id="email"
          placeholder="Input Email"
          v-model="email"
        />
        <span v-if="errors.email" class="error">{{ errors.email }}</span>
      </div>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>
