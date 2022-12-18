<script setup>
import {inject} from "vue";
const props = defineProps({
    name: {
        type: String,
        required: true
    },
    as: {
        type: String,
        required: false
    },
    modelValue: {
        type: String,
        required: false,
        default: '',
    },
});
const {updateValue} = inject('updateValue');
</script>

<template>
    <component :is="as" :name="name" @input="updateValue(name, $event.target.value)">
        <slot />
    </component>
</template>