<template>
  
  <div v-if="loading" class="loading-page">
    <div class="loading"></div>
  </div>
</template>

<script>
export default {
  data: () => ({
    loading: false
  }),
  methods: {
    start() {
      this.loading = true
    },
    finish() {
      this.loading = false
    }
  }
}
</script>

<style scoped>

.loading-page {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-image: url('./../static/Loader.gif');
  background-repeat: no-repeat;
  z-index: 999;
}
</style>
