<template>
  <v-container>
     <v-alert type="error">
       <h1>Oops, looks like something went wrong!</h1>
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
    name: "SubmissionFail"
  }
</script>