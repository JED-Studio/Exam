<script>
import { defineComponent, ref } from 'vue'
import AppBasket from './AppBasket.vue'

export default defineComponent({
  components: {
    AppBasket,
  },
  setup() {
    const isBasketOpen = ref(false)
    const toggleBasket = () => {
      isBasketOpen.value = !isBasketOpen.value
    }

    const basketItems = ref([])
    const availableItems = ref([
      {
        id: 1,
        name: 'iPhone',
        price: 300,
      },
      {
        id: 2,
        name: 'Xiaomi',
        price: 200,
      },
      {
        id: 3,
        name: 'Huawei',
        price: 100,
      },
    ])

    const addToBasket = (item) => {
      const existingItem = basketItems.value.find((basketItem) => basketItem.id === item.id)
      if (existingItem) {
        existingItem.quantity += 1
      } else {
        basketItems.value.push({
          id: item.id,
          name: item.name,
          price: item.price,
          quantity: 1,
        })
      }
    }

    const calculateTotal = () => {
      return basketItems.value.reduce((total, item) => total + item.price * item.quantity, 0)
    }

    const updateItemQuantity = (item, change) => {
      const currentItem = basketItems.value.find((basketItem) => basketItem.id === item.id)
      if (currentItem) {
        currentItem.quantity += change
        if (currentItem.quantity <= 0) {
          basketItems.value = basketItems.value.filter((basketItem) => basketItem.id !== item.id)
        }
      }
    }

    return {
      isBasketOpen,
      toggleBasket,
      addToBasket,
      calculateTotal,
      basketItems,
      availableItems,
      updateItemQuantity,
    }
  },
})
</script>

<template>
  <div>
    <div @click="toggleBasket">Корзина</div>
    <div v-for="item in availableItems" :key="item.id">
      {{ item.name }} - {{ item.price }}₽
      <div @click="addToBasket(item)">Купить</div>
    </div>
  </div>
  <div class="basket" :class="{ 'basket--active': isBasketOpen }">
    <AppBasket :basket="basketItems" @updateQuantity="updateItemQuantity" />
    Итого: {{ calculateTotal() }}₽
  </div>
</template>

<style scoped>
.basket {
  position: fixed;
  width: 300px;
  background-color: aqua;
  top: 0;
  right: 0;
  height: 100%;
}

.basket--active {
  right: -300px;
}
</style>
