<template>
  <label v-if="label">{{ label }} </label>
  <select
    :value="modelValue"
    class="field"
    v-bind="{
      ...$attrs,
      onChange: ($event) => {
        $emit('update:modelValue', $event.target.value);
      },
    }"
  >
    <option
      v-for="opcion in opciones"
      :value="opcion"
      :key="opcion"
      :selected="opcion === modelValue"
    >
      {{ opcion }}
    </option>
  </select>
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
    opciones: {
      type: Array,
      required: true,
    },
    error: {
      type: String,
      default: "",
    },
  },
};
</script>