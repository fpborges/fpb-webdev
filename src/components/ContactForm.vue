<template>
  <v-form @submit.prevent="handleSubmit" name="contact" method="POST" netfly-honeypot="bot-field" data-netlify="true" v-model="valid">
    <v-container>
        <p hidden class="hidden">
        <label>Are you Human? <input name="bot-field" /></label>   
      </p>
      <v-row>
        <v-col
          cols="3"
          md="4"
        >
          <v-text-field
            v-model="firstname"
            name="firstname"
            :rules="nameRules"
            :counter="10"
            label="First name"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="3"
          md="4"
        >
          <v-text-field
            v-model="lastname"
            name="lastname"
            :rules="nameRules"
            :counter="10"
            label="Last name"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="3"
          md="4"
        >
          <v-text-field
            v-model="email"
            name="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
        </v-col>
        <v-col
          cols="3"
          md="4"
        >
          <v-textarea
            v-model="message"
            name="message"
            :rules="messageRules"
            label="Message"
            required
          ></v-textarea>
        </v-col>
      </v-row>
          <v-btn
        :disabled="!valid"
        type="submit"
        color="primary"
        class="mr-4"
      >
        Submit
      </v-btn>
 
    </v-container>
  </v-form>
</template>

<script>
  export default {
    name: "QAForm",
    data: () => ({
      valid: false,
      firstname: '',
      lastname: '',
      message:'',
      messageRules: [
        v => !!v || 'Message is required',
        v => v.length >= 10 || 'Message must have more than 10 characters',
      ],
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),
    methods:{
        encode(data){
            return Object.keys(data).map(key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`).join('&')
        },
        handleSubmit() {
            fetch('/', {
                method: 'post',
                headers:{
                    'Content-Type': 'application/x-www-urlencoded'
                },
                body: this.encode({
                    'form-name': 'contact',
                    ...this.form
                })
            })
            .then(() => console.log('success'))
            .catch(e => console.error(e))
        }
    }
  }
</script>


