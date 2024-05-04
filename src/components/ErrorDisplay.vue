<template>
  <div class="error-display" v-if="error">
    <h3>{{ error }}</h3>
  </div>
</template>

<script>
export default {
  props: {
    error: String
  }
};
</script>

<style scoped>
.error-display {
  color: red;
  text-align: center;
  margin-bottom: 20px;
}
</style>
