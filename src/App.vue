<template>
  <div id="app">
    <buck :bucks="bucks" :disabled="!isStart" @click="event" />
    <div v-if="!isStart" class="start-game" @click="isStart = true">Начать</div>
    <timer
      v-else
      class="timer"
      :answer="answer"
      :current-trash="currentTrash.value"
    />
  </div>
</template>

<script>
import buck from "./components/buck.vue"
import timer from "./components/timer.vue"

export default {
  name: "App",
  components: {
    buck,
    timer,
  },

  data: () => ({
    isStart: false,
    gameOver: false,
    trash: [],
    answer: {
      right: 0,
      wrong: 0,
    },
    currentTrash: {},
    bucks: [
      {
        name: "orange",
        img: "bucks/wastebox_orange.png",
        title: "Смешанные",
        isOpen: false,
        top: "bucks/buck_top/wastetop_orange.png",
      },
      {
        name: "green",
        isOpen: false,
        img: "bucks/wastebox_green.png",
        title: "Вторсырьё",
        top: "bucks/buck_top/wastetop_green.png",
      },
      {
        name: "blue",
        isOpen: false,
        img: "bucks/wastebox_blue.png",
        title: "Бытовые",
        top: "bucks/buck_top/wastetop_blue.png",
      },
      {
        name: "red",
        isOpen: false,
        img: "bucks/wastebox_red.png",
        title: "Опасные",
        top: "bucks/buck_top/wastetop_red.png",
      },
    ],
  }),

  async mounted() {
    await this.initFetch()
  },

  methods: {
    async initFetch() {
      const response = await fetch("/trash.json")
      const trash = await response.json()
      this.trashLength = trash.length
      this.trash = trash[Symbol.iterator]()
      this.currentTrash = this.trash.next()
    },

    event(e) {
      if (!this.isStart) {
        return
      }
      console.log(this.currentTrash)
      if (this.currentTrash.done === true) {
        this.gameOver = true
        this.isStart = false
        this.initFetch()
        this.answer = {
          right: 0,
          wrong: 0,
        }
        console.log(this.gameOver)
      }

      this.currentTrash.value.value === e
        ? this.answer.right++
        : this.answer.wrong++

      this.currentTrash = this.trash.next()
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column-reverse;
  align-items: center;
}

.start-game {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: auto;
  margin-top: 100px;
  height: 400px;
  width: 400px;
  text-align: center;
  background: white;
  font-size: 50px;
  border-radius: 50%;
}
</style>
