<template>
  <div class="loader"></div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "./assets/variables.scss";
.loader {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.loader:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 8px solid $text-color;
  border-color: $text-color transparent $text-color transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
