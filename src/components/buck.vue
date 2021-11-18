<template>
  <div class="bucks" :class="{ disabled: disabled }">
    <div
      v-for="(buck, index) in bucks"
      :key="index"
      class="buck"
      @click="$emit('click', buck.title)"
      @mouseup="openBuck(index)"
    >
      <div class="title" :style="{ backgroundColor: buck.name }">
        {{ buck.title }}
      </div>
      <transition name="fade">
        <img
          class="top"
          :style="!buck.isOpen ? { marginTop: 40 + 'px' } : null"
          :src="require(`@/assets/${buck.top}`)"
        />
      </transition>
      <img class="body" :src="require(`@/assets/${buck.img}`)" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    bucks: {
      type: Array,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  data: () => ({
    isOpen: true,
  }),

  methods: {
    openBuck(index) {
      this.bucks[index].isOpen = !this.bucks[index].isOpen
      setTimeout(() => (this.bucks[index].isOpen = false), 200)
    },
  },
}
</script>

<style>
.disabled {
  pointer-events: none;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}

.bucks {
  display: flex;
  margin-top: 50px;
  user-select: none;
}

.buck {
  width: 150px;
  cursor: pointer;
  margin-left: 10px;
  display: flex;
  flex-direction: column;
}

.top {
  width: 110px;
  align-self: center;
  z-index: -1;
  position: absolute;
}

.title {
  color: white;
  z-index: -2;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  border-radius: 15px;
  margin-bottom: 15px;
}

.body {
  width: 150px;
}
</style>