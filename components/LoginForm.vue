<template>
  <v-card width="100%" v-if="!forgotScreen">
    <v-card-title>
      <div>
        <div class="text-h5 grey--text">DEFCON OS</div>
        <div class="text-subtitle-1 accent--text">Fast, encrypted and free farm tracking</div>
      </div>
    </v-card-title>
    <v-card-text class="px-0">
      <v-container fluid class="p-0">
        <v-row class="mb-2" no-gutters>
          <v-col>
            <v-text-field 
              outlined 
              hide-details 
              dense
              placeholder="Grid ID"
              label="Grid ID"
              v-model="username"
            />
          </v-col>
        </v-row>
        <v-row no-gutters>
          <v-col>
            <v-text-field 
              outlined 
              hide-details 
              dense 
              placeholder="Grid Key"
              label="Grid Key"
              type="password"
              v-model="password"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions class="px-0">
      <v-container fluid style="width: 100%;" class="p-0">
        <v-row no-gutters>
          <v-col cols="12">
            <v-btn 
              width="100%" 
              class="mb-2"
              color="blue"
              @click="login"
              text
            >
              Login
            </v-btn>
          </v-col>
        </v-row>
        <v-row no-gutters>
          <v-col cols="12">
            <v-btn 
              width="100%" 
              class="mb-2"
              color="green"
              @click="forgotScreen = true"
              text
            >
              Forgot Password?
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-card-actions>
  </v-card>
  <v-card width="100%" v-else>
    <v-card-title class="d-flex">
      <p class="ma-0 pa-0">Password Reset</p>
    </v-card-title>
    <v-card-text class="px-0">
      <v-container fluid class="p-0">
        <v-row class="mb-2" no-gutters>
          <v-col>
            <v-form ref="form" v-model="form">
              <v-text-field 
                outlined
                dense
                placeholder="Grid Email"
                :rules="[rules.required, rules.email]"
                label="E-mail"
                v-model="email"
              />
            </v-form>
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions class="px-0">
      <v-container fluid style="width: 100%;" class="p-0">
        <v-row no-gutters>
          <v-col cols="12">
            <v-btn 
              width="100%" 
              class="mb-2"
              color="blue"
              @click="resetPass"
            >
              Submit
            </v-btn>
          </v-col>
        </v-row>
        <v-row no-gutters>
          <v-col cols="12">
            <v-btn 
              width="100%" 
              class="mb-2"
              @click="forgotScreen = false"
            >
              Go back
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      email: "",
      form: false,
      forgotScreen: false,
      rules: {
        required: value => !!value || 'Required.',
        counter: value => value.length <= 20 || 'Max 20 characters',
        email: value => {
          const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
          return pattern.test(value) || 'Invalid e-mail.'
        },
      },
    }
  }, 
  methods: {
    login() {
      if (this.username === "HIVE-220-972-9501" && this.password === "jfepucid998sikqpv40to") {
        this.$emit("loggedIn", true)
      } else {
        this.$emit("loggedIn", false)
      }
    },
    resetPass() {
      this.$refs.form.validate()
      if (this.form) this.$emit("reset", true)
    },
  },
  created() {

  },
}
</script>