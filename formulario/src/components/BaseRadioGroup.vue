<template>
  <component
    v-for="opcion in opciones"
    :key="opcion.value"
    :is="vertical ? 'div' : 'span'"
    :class="{
      horizontal: !vertical,
    }"
  >
    <BaseRadiobutton
      :label="opcion.label"
      :value="opcion.value"
      :name="name"
      :modelValue="modelValue"
      @update:modelValue="$emit('update:modelValue', $event)"
    />
  </component>
</template>

<script>
export default {
  props: {
    opciones: {
      Type: Array,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    modelValue: {
      type: [String, Number],
      required: true,
    },
    vertical: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
.horizontal {
  margin-right: 18px;
}
</style>