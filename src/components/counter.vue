<template>
  <div class="counter">
    <div class="right"></div>
    <div class="wrong"></div>
  </div>
</template>

<script>
export default {
  props: {
    answer: {
      type: Boolean,
    },
  },
}
</script>

<style>
.counter {
  display: flex;
}

.right {
  width: 50px;
  height: 50px;
  background-color: green;
}

.wrong {
  width: 50px;
  height: 50px;
  background-color: red;
}
</style>