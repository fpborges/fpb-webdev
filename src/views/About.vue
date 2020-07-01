<template>
  <div class="about">
    <AboutComponent />
    <h1>This is an about page</h1>
  </div>
</template>

<script>
import AboutComponent from '@/components/AboutComponent.vue'

export default {
  name: 'About',
  components: {
    AboutComponent
  }
}

</script>
