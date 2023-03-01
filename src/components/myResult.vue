<template>
  <div class="result-container">
    <h2>{{ message }}</h2>
    <h3>Game is Over</h3>
    <button @click="$emit('refresh')">
      <img src="../assets/refresh-icon.png" alt="" />
    </button>
  </div>
</template>
<script>
export default {
  props: ["message"],
};
</script>
<style scoped>
.result-container {
  position: absolute;
  gap: 10px;
  background-color: #fbb500;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  color: blueviolet;
}
.result-container button {
  position: relative;
  bottom: 0;
}
</style>
