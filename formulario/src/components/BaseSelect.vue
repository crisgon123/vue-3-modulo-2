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
</template>

<script>
export default {
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
  },
};
</script>