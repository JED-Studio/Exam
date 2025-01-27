<script>
import { defineComponent } from 'vue'
import AppButton from './AppButton.vue'

export default defineComponent({
  components: {
    AppButton,
  },
  setup() {},
})
</script>

<template>
  <AppButton>
    <template #default> пицца </template>
  </AppButton>
  <AppButton>
    <template #default> шаурма </template>
  </AppButton>
</template>
