<template>
  <select :value="modelValue" @change="optionChanger">
    <option disabled value="">Select</option>
    <option v-for="option in options" :value="option.value" :key="option.value">
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'my-options',
  props: {
    modelValue: { type: String },
    options: { type: Array, default: () => [] },
  },

  methods: {
    optionChanger(event) {
      this.$emit('update:modelValue', event.target.value)
    },
  },
}
</script>

<style scoped>
select {
  border: 1px solid teal;
  border-radius: 8px;
  height: 50px;
  color: teal;
  margin-top: 10px;
}
</style>