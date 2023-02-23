<template>
  <main>
    <form @submit="onSubmit">
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
      <div class="">
        <label for="rememberMe">rememberMe</label>
        <input
          id="rememberMe"
          v-model="rememberMe"
          type="checkbox"
          placeholder=""
        />
      </div>
      <button type="submit">Войти</button>
    </form>
  </main>
</template>

<script setup lang="ts">
import { useField, useForm } from 'vee-validate';
import * as yup from 'yup';

useHead({
  title: 'Авторизация',
});

definePageMeta({
  layout: 'empty',
});

const signInSchema = yup.object({
  email: yup
    .string()
    .min(1, 'Email address is required')
    .email('Email Address is invalid'),
  password: yup
    .string()
    .min(1, 'Password is required')
    .min(8, 'Password must be more than 8 characters')
    .max(32, 'Password must be less than 32 characters'),
  rememberMe: yup.boolean(),
});

const { handleSubmit, errors, resetForm } = useForm({
  validationSchema: signInSchema,
});

const { value: email } = useField('email');
const { value: password } = useField('password');
const { value: rememberMe } = useField('rememberMe');

const onSubmit = handleSubmit((values) => {
  console.log('email: ', values.email);
  console.log('password: ', values.password);
  console.log('rememberMe: ', values.rememberMe);
  resetForm();
});
</script>

<style scoped></style>
