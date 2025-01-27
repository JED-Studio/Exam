<script>
import { defineComponent } from 'vue'
import AppSidebar from './components/sidebar/AppSidebar.vue'
import AppCard from './components/shop/AppCard.vue'
export default defineComponent({
  components: {
    AppSidebar,
    AppCard,
  },
})
</script>

<template>
  <div>
    <div class="exam__appsidebar">
      <div class="exam__container">
        <div>1 экзамен</div>
        <AppSidebar />
      </div>
    </div>
    <div class="exam__shop">
      <div class="exam__container">
        <div>2 экзамен</div>
        <AppCard />
      </div>
    </div>
  </div>
</template>

<style>
.exam__container {
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
  padding: 0 20px;
}
</style>
