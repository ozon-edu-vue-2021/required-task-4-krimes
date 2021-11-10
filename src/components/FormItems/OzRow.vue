<template>
  <div class="row">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Row",
};
</script>

<style scoped>
.row {
  display: flex;
  margin-bottom: 20px;
}
</style>
