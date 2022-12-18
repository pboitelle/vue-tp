<script setup>
import { ref } from 'vue';
import FormikVue from './components/Formik.vue';
import Field from './components/Field.vue';

const initialValues = {
  email: '',
  password: '',
};

const errorsValues = ref({});

const validate = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = 'Email is required !';
  } else if (!/\S+@\S+\.\S+/.test(values.email)) {
    errors.email = 'Invalid email address';

  }
  if (!values.password) {
    errors.password = 'Password required !';
  } else if (values.password.length < 8) {
    errors.password = 'Must be 8 characters or more';
  }

  errorsValues.value = errors;
  return errors;
};

const onSubmit = (values) => {
  alert(JSON.stringify(values, null, 2));
};

</script>

<template>
  <main>
    <FormikVue 
      :initialValues="initialValues"
      :validate="validate"
      :onSubmit="onSubmit"
    >

        <h1>Formik Vue</h1>

        <label for="Email">Email</label>
        <Field
          as="input"
          name="email"
          type="email"
        />
        <div v-if="errorsValues.email"
        style="color: red">
          {{ errorsValues.email }}
        </div>

        <label for="Password">Password</label>
        <Field
          as="input"
          name="password"
          type="password"
        />
        <div v-if="errorsValues.password"
        style="color: red">
          {{ errorsValues.password }}
        </div>

        <Field
          as="button"
          type="submit"
          name="submit">
          Submit
        </Field>

    </FormikVue>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

main {
  display: flex;
  flex-direction: column;
  place-items: center;
  padding: 0 var(--section-gap);
}

@media (min-width: 1024px) {
  main {
    flex-direction: row;
    place-items: flex-start;
    padding: 0 calc(var(--section-gap) / 2);
  }
}

h1 {
  font-size: 2rem;
  font-weight: 400;
  margin: 0 0 1rem;
}

label {
  display: block;
  font-size: 1.25rem;
  font-weight: 400;
  margin: 0 0 0.5rem;
}

input {
  border: 1px solid #ccc;
  border-radius: 4px;
  display: block;
  font-size: 1rem;
  padding: 0.5rem;
  width: 100%;
}

button {
  background-color: #4caf50;
  border: none;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;
  font-size: 1rem;
  padding: 0.5rem;
}

button:hover {
  background-color: #45a049;
}
</style>
