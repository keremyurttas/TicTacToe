<template>
  <div class="result-container">
    <h2>{{ message }}</h2>
    <h3>Game is Over</h3>
    <button class="refresh" @click="$emit('refresh')">
      <img src="../assets/refresh.svg" alt="" />
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
  gap: 20px;
  background-color: #c286ff;
  height: 80%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  color: white;
  border-radius: 20px;
  border: 3px solid white;
  border-bottom: #a75cf4 solid 6px;
}
.result-container button {
  position: relative;
  bottom: 0;
}
.result-container h2 {
  text-shadow: 0px 2px 0px #e546ff;
  font-size: 2rem;
}
.refresh {
  border-radius: 50px;
  aspect-ratio: 1;

  padding: 0.5rem;
  background-color: #92f200;
  border: solid 8px white;
  box-shadow: 0 6px #39bd01;
}
</style>
