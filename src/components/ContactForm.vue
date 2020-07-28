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
            v-model="form.firstname"
            name="firstname"
            type="text"
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
            v-model="form.lastname"
            name="lastname"
            type="text"
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
            v-model="form.email"
            name="email"
            type="email"
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
            v-model="form.message"
            name="message"
            type="text"
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
      <v-row>
        {{ formCallBack }}
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
  import axios from "axios";
  export default {
    name: "QAForm",
    data: () => ({
      valid: false,
      formCallBack: '',
      savingSuccessful: false,
      form:{
        firstname: '',
        lastname: '',
        email: '',
        message:'',
      },
      messageRules: [
        v => !!v || 'Message is required',
        v => v.length >= 10 || 'Message must have more than 10 characters',
      ],
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),
    methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    handleSubmit() {
      const axiosConfig = {
        header: { "Content-Type": "application/x-www-form-urlencoded" }
      };
      axios.post(
        "/",
        this.encode({
          "form-name": "contact",
          ...this.form
        }),
        axiosConfig
      ).then(() => {
        this.$router.push('thanks')        
      })
      .catch(() => {
        this.$router.push('404')
        })
      }
    }
  }
</script>

//onSubmit() {
// 		this.form.post('/projects')
// 			.then(response => alert('Wahoo!'));
// 	}