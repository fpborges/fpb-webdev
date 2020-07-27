<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <HomeBody msg="Welcome to Your Vue.js App"/>
    <QAForm/>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeBody from '@/components/HomeBody.vue'
import QAForm from '@/components/ContactForm.vue'

export default {
  name: 'Home',
  components: {
    HomeBody,
    QAForm
  }
}
</script>

<style scoped>
  a{
    font-weight: bold;
  }
</style>