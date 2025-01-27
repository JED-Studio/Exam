<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    const open = ref(false)
    const option = () => {
      open.value = !open.value
    }

    return {
      open,
      option,
    }
  },
})
</script>

<template>
  <div class="exam__sidebar" :class="{ 'exam-sidebar--active': !open }">
    <div @click="option">close</div>
    <slot></slot>
  </div>
  <button @click="option">open</button>
</template>

<style>
.exam__sidebar {
  position: fixed;
  width: 300px;
  background-color: aqua;
  top: 0;
  left: 0;
  height: 100%;
}

.exam-sidebar--active {
  left: -300px;
}
</style>
