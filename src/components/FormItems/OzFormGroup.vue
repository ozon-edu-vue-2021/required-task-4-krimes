<template>
  <div class="oz-form-group">
    <div v-if="$slots.label" class="oz-form-group__label">
      <slot name="label"></slot>
    </div>
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>

<style>
.oz-form-group {
  padding-right: 20px;
}

.oz-form-group__label {
  padding-bottom: 10px;
  color: #8190a4;
  font-size: 20px;
}
</style>
