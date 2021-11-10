<template>
  <oz-input
    type="date"
    class="oz-date-input"
    placeholder="дд.мм.гггг"
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
.oz-date-input {
  width: 400px;
}
</style>
