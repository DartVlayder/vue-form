<template>
  <div class="home">
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
<style lang="scss" scoped>
  .home {
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
  }
</style>