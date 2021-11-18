<template>
  <div class="timer">
    <div class="right">{{ answer.right }}</div>
    <div class="wrong">{{ answer.wrong }}</div>
    <div id="countdown">
      <div v-if="currentTrash" class="trash">{{ currentTrash.name }}</div>
      <svg>
        <circle r="180" cx="200" cy="200"></circle>
      </svg>
    </div>
  </div>
</template>




<script>
export default {
  props: {
    currentTrash: {
      type: Object,
    },
    answer: {
      type: Object,
    },
  },
  mounted() {
    let countdown = 60

    let timer = setInterval(function () {
      countdown = --countdown <= 0 ? clearInterval(timer) : countdown
    }, 1000)
  },
}
</script>

<style>
body {
  height: 100%;
  width: 100%;
  background-color: #333;
}

.timer {
  display: flex;
  margin-top: 100px;
  align-items: center;
}

.right {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  font-size: 40px;
  color: white;
  height: 50px;
  background-color: green;
}

.wrong {
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  font-size: 40px;
  width: 50px;
  order: 1;
  height: 50px;
  background-color: red;
}

#countdown {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: auto;
  height: 400px;
  width: 400px;
  text-align: center;
}

.trash {
  color: white;
  font-size: 40px;
  display: inline-block;
  line-height: 40px;
}

svg {
  position: absolute;
  top: 0;
  right: 0;
  width: 400px;
  height: 400px;
  transform: rotateY(-180deg) rotateZ(-90deg);
}

svg circle {
  stroke-dasharray: 1130px;
  stroke-dashoffset: 0px;
  stroke-linecap: round;
  stroke-width: 20px;
  stroke: white;
  fill: none;
  animation: countdown 60s linear infinite forwards;
}

@keyframes countdown {
  from {
    stroke-dashoffset: 0px;
  }
  to {
    stroke-dashoffset: 1130px;
  }
}
</style>