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

        <v-dialog
      v-model="dialog"
      max-width="290"
    >
      <v-card>
      
        <v-card-text>
           <v-alert type="success" v-model= "alertSuccess">
            I'm a success alert.
            </v-alert>
            <v-alert type="error" v-model= "alertError">
            I'm an error alert.
        </v-alert> 
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn
            color="green darken-1"
            
            text
            @click="dialog = false, reloadPage()"
          >
            OK
          </v-btn>

          <v-btn
            color="green darken-1"
            text
            @click="dialog = false"
          >
            Agree
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
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
      alertError: false,
      alertSuccess: false,
      dialog: false,
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
    reloadPage(){
    window.location.reload()
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
        this.alertSuccess= true;
        
      })
      .catch(() => {
        // alert("Error!!");
        // this.form.reset();
        this.alertError= true;
        this.dialog= true;
   
        // this.$router.go('/');
        })
      }
    }
  }
</script>

