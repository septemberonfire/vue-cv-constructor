<script>
export default {
  props: {
    avatarUrl: String
  }
}
</script>

<template>
  <div class="avatar">
    <img
      :src="avatarUrl" alt="avatar"/>
  </div>
</template>

<style>

</style>
