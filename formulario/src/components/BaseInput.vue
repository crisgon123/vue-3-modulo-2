<template>
  <label :for="uuid">{{ label }} </label>
  <input
    v-bind="$attrs"
    :placeholder="label"
    class="field"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    :id="uuid"
    :aria-describedby="error ? `${uuid}-error` : null"
    aria-live="assertive"
    :aria-invalid="error ? true : null"
  />
  <p v-if="error" class="errorMessage" :id="`${uuid}-error`">
    {{ error }}
  </p>
</template>

<script>
import UniqueID from "../UniqueID";
export default {
  data() {
    return {
      uuid: UniqueID(),
    };
  },
  props: {
    label: {
      type: String,
      default: "",
    },
    modelValue: {
      type: [String, Number],
      default: "",
    },
    error: {
      type: String,
      default: "",
    },
  },
};
</script>