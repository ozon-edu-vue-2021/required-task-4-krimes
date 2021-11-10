<template>
  <oz-input
    class="oz-email-input"
    id="email"
    placeholder=""
    :value="value"
    @input="$emit('input', $event)"
  >
  </oz-input>
</template>

<script>
import { OzInput } from "./";
export default {
  components: { OzInput },
  model: {
    prop: "value",
    event: "input",
  },

  props: {
    value: {
      type: String,
      default: "",
    },
  },
};
</script>

<style>
.oz-email-input {
  
}
</style>
