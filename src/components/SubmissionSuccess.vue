<template>
  <v-container>
     <v-alert type="success">
      <h1>You're Awesome! Thank you for your submission!</h1>
    </v-alert>
    <router-link to="/">
      <div class="my-2">
        <v-btn color="primary" dark large>Back To Page</v-btn>
      </div>
    </router-link>
  </v-container>
</template>

<script>
  export default {
    name: "SubmissionSuccess"
  }
</script>