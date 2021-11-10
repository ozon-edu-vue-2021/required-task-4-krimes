<template>
  <div class="oz-radio-group">
    <div v-for="(radio, index) of items" :key="radio">
      <input
        type="radio"
        v-bind="$attrs"
        :id="`radio-${radio}-${index}`"
        class="oz-radio-input"
        :value="radio"
        v-model="modelValue"
      />
      <label :for="`radio-${radio}-${index}`">{{ radio }}</label>
    </div>
  </div>
</template>

<script>
// import { OzInput } from "./";
export default {
  // components: { OzInput },
  model: {
    prop: "value",
    event: "input",
  },

  props: {
    value: {
      type: String,
      default: "",
    },
    items: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    modelValue: {
      get() {
        return this.value
      },
      set(value) {
        this.$emit('input', value)
      },
    }
  }
};
</script>

<style>
.oz-radio-group {
  display: flex;
}
</style>
