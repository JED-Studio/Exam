<script>
import { defineComponent, ref } from 'vue'
import AppBasket from './AppBasket.vue'

export default defineComponent({
  components: {
    AppBasket,
  },
  setup() {
    const openBasket = ref(false)
    const optionBasket = () => {
      openBasket.value = !openBasket.value
    }

    const basket = ref([])
    const items = ref([
      {
        id: 1,
        name: 'iphone',
        price: 300,
      },
      {
        id: 2,
        name: 'xiaomi',
        price: 200,
      },
      {
        id: 3,
        name: 'huawei',
        price: 100,
      },
    ])

    const pushBasket = (item) => {
      const upBasket = basket.value.find((basketItem) => basketItem.id === item.id)
      if (upBasket) {
        upBasket.question += 1
      } else {
        basket.value.push({
          id: item.id,
          name: item.name,
          price: item.price,
          question: 1,
        })
      }
    }

    const result = () => {
      return basket.value.reduce((total, item) => total + item.price * item.question, 0)
    }

    const prev = (item, chart) => {
      const current = basket.value.find((pol) => pol.id === item.id)
      if (current) {
        current.question += chart
        if (current.question <= 0) {
          basket.value = basket.value.filter((pol) => pol.id !== item.id)
        }
      }
    }

    return {
      openBasket,
      optionBasket,
      pushBasket,
      result,
      basket,
      items,
      prev,
    }
  },
})
</script>

<template>
  <div>
    <div @click="optionBasket">basket</div>
    <div v-for="item in items" :key="item">
      {{ item.name }}-{{ item.price }}
      <div @click="pushBasket(item)">Купить</div>
    </div>
  </div>
  <div class="exam__basket" :class="{ 'exam-basket--active': openBasket }">
    <AppBasket :basket="basket" @prev="prev" />
    {{ result() }}
  </div>
</template>

<style scoped>
.exam__basket {
  position: fixed;
  width: 300px;
  background-color: aqua;
  top: 0;
  right: 0;
  height: 100%;
}

.exam-basket--active {
  right: -300px;
}
</style>
