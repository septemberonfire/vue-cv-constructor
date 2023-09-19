<script>
export default {
  props: {
    type: String,
  },
};
</script>

<template>
  <h1 v-if="type === 'title'"><slot></slot></h1>
  <h2 v-else-if="type === 'subtitle'"><slot></slot></h2>
  <p v-else><slot></slot></p>
</template>

<style></style>
