<script lang="ts">
import AgeCard from './components/AgeCard.vue'

export default {
  components: {
    Card: AgeCard,
  },
}
</script>

<template>
  <div class="container">
    <Card/>
  </div>
</template>

<style lang="scss" scoped>
.container {
  background-color: var(--off-white);
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;

}
</style>
