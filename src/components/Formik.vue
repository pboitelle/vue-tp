<template>
  <form @submit.prevent="handleSubmit">
    <slot />
  </form>
</template>

<script setup>
import { provide, reactive } from "vue";
const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  onSubmit: {
    type: Function,
    required: true,
  },
  validate: {
    type: Function,
    required: false,
  },
});

const values = reactive(props.initialValues);
const updateValue = (field, value) => {
  values[field] = value;
};
provide('updateValue', {updateValue});

const errors = reactive({});
provide('errors', errors);

const handleSubmit = (e) => {
  e.preventDefault();

  if (props.validate) {
    const errorsVal = props.validate(values);

    if (Object.keys(errorsVal).length > 0) {
      Object.assign(errors, errorsVal);
      console.log(errors)
      return;
    }
  }

  props.onSubmit(values);
};
</script>