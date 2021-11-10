<template>
  <input
    class="oz-input"
    v-bind="$attrs"
    :value="value"
    v-on="{
      ...$listeners,
      input: (event) => $emit('input', event.target.value),
    }"
  />
</template>

<script>
export default {
  model: {
    prop: "value",
    event: "input",
  },
  props: {
    value: {
      type: String,
    },
  },
};
</script>

<style>
.oz-input {
  width: 100%;
  border: 5px solid #dae0e5;
  border-radius: 5px;
  font-size: 18px;
  padding: 10px;
}

.oz-input:hover {
  border: 5px solid #c1c5c9;
  border-radius: 5px;
}

.oz-input:focus {
  outline: none;
}
</style>
