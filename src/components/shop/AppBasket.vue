=
<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    basket: Array,
  },

  setup(__, { emit }) {
    const updateQuantity = (item, change) => {
      emit('updateQuantity', item, change)
    }

    return {
      updateQuantity,
    }
  },
})
</script>

<template>
  <div v-for="item in basket" :key="item.id">
    {{ item.name }} {{ item.price }}₽
    <div class="basket-item">
      <div @click="updateQuantity(item, -1)">-</div>
      <div>{{ item.quantity }}</div>
      <div @click="updateQuantity(item, 1)">+</div>
    </div>
  </div>
</template>
