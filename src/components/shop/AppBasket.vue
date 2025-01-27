<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    basket: Array,
  },

  setup(__, { emit }) {
    const prev = (item, chart) => {
      emit('prev', item, chart)
    }

    return {
      prev,
    }
  },
})
</script>

<template>
  <div v-for="item in basket" :key="item">
    {{ item.name }} {{ item.price }}
    <div class="exam__basket">
      <div @click="prev(item, -1)">-</div>
      <div>{{ item.question }}</div>
      <div @click="prev(item, 1)">+</div>
    </div>
  </div>
</template>
