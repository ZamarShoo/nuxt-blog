<template>
    <div class="empty-layout">
      <nuxt />
    </div>
</template>

<script>
    export default {
        name: "empty"
    }
</script>

<style lang="scss" scoped>
  .empty-layout {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
  }
</style>
