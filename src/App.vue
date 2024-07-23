<script setup>
import { defineRule, Form, Field, ErrorMessage, configure } from 'vee-validate';
import { required, between, confirmed } from '@vee-validate/rules';
import { localize } from '@vee-validate/i18n';
import pt_BR from '@vee-validate/i18n/dist/locale/pt_BR.json';

// define global rules
defineRule('required', required);
defineRule('between', between);
defineRule('confirmed', confirmed);

localize({ pt_BR });

// Activate the locale
configure({
  generateMessage: localize('pt_BR', {
    names: {
      name: 'Nome',
      age: 'Idade',
      ageConfirm: 'Confirmar idade',
    },
  }),
});

function onSubmit(values) {
  alert(JSON.stringify(values, null, 2));
}
</script>

<template>
  <Form @submit="onSubmit">
    <label for="name">Nome</label>
    <Field name="name" type="text" rules="required" />
    <ErrorMessage name="name" />

    <label for="name">Idade</label>
    <Field name="age" type="number" rules="required|between:18,96" />
    <ErrorMessage name="age" />

    <label for="name">Confirmar idade</label>
    <Field name="ageConfirm" type="number" rules="required|confirmed:@age" />
    <ErrorMessage name="ageConfirm" />

    <button>Enviar</button>
  </Form>
</template>

<style scoped>
span,
button {
  display: block;
  margin: 10px 0;
}

label {
  display: block;
}
</style>
