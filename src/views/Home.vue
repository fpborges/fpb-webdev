<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <HomeBody msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeBody from '@/components/HomeBody.vue'

export default {
  name: 'Home',
  components: {
    HomeBody
  }
}
</script>

<style scoped>
  a{
    font-weight: bold;
  }
</style>