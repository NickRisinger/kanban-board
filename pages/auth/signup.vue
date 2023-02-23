<template>
  <main>
    <form @submit="onSubmit">
      <div class="">
        <label for="firstName">firstName</label>
        <input
          id="firstName"
          v-model="firstName"
          type="text"
          placeholder="Введите email"
        />
        <span>{{ errors.firstName }}</span>
      </div>
      <div class="">
        <label for="lastName">lastName</label>
        <input
          id="lastName"
          v-model="lastName"
          type="text"
          placeholder="Введите email"
        />
        <span>{{ errors.lastName }}</span>
      </div>
      <div class="">
        <label for="email">email</label>
        <input
          id="email"
          v-model="email"
          type="email"
          placeholder="Введите email"
        />
        <span>{{ errors.email }}</span>
      </div>
      <div class="">
        <label for="password">Password</label>
        <input
          id="password"
          v-model="password"
          type="password"
          placeholder=" "
        />
        <span>{{ errors.password }}</span>
      </div>
      <button type="submit">Войти</button>
    </form>
  </main>
</template>

<script setup lang="ts">
import { useField, useForm } from 'vee-validate';
import * as yup from 'yup';

useHead({
  title: 'Регистрация',
});

definePageMeta({
  layout: 'empty',
});

const signInSchema = yup.object({
  email: yup
    .string()
    .min(1, 'Email address is required')
    .email('Email Address is invalid'),
  firstName: yup.string(),
  lastName: yup.string(),
  password: yup
    .string()
    .min(1, 'Password is required')
    .min(8, 'Password must be more than 8 characters')
    .max(32, 'Password must be less than 32 characters'),
});

const { handleSubmit, errors, resetForm } = useForm({
  validationSchema: signInSchema,
});

const { value: email } = useField('email');
const { value: firstName } = useField('firstName');
const { value: lastName } = useField('LastName');
const { value: password } = useField('password');

const onSubmit = handleSubmit((values) => {
  console.log('email: ', values.email);
  console.log('password: ', values.password);
  resetForm();
});
</script>

<style scoped></style>
