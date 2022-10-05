<template>
  <div>
    <div>
      <login-form v-if="!loggedIn" @loggedIn="tryLogin" @reset="sendReset" />
    </div>
    <v-skeleton-loader
      v-bind="attrs"
      type="actions"
      v-if="loading"
    ></v-skeleton-loader>
    <v-skeleton-loader
      v-bind="attrs"
      type="date-picker"
      v-if="loading"
    ></v-skeleton-loader>
    <Dashboard
      v-if="!loading && loggedIn"
    />
    <v-snackbar
      v-model="snackBar"
      timeout="2000"
      :color="snackColor"
      top
    >
      {{ snackText }}
    </v-snackbar>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard.vue';
import LoginForm from '../components/LoginForm.vue';

export default {
  name: 'IndexPage',
  components: { LoginForm, Dashboard },
  data() {
    return {
      loggedIn: false,
      loading: false,
      snackText: "",
      snackColor: "",
      snackBar: false,
      attrs: {
        class: 'mb-6',
        // boilerplate: true,
        elevation: 2,
      },
    }
  },
  methods: {
    callSnackBar(text, color) {
      this.snackText = text
      this.snackColor = color
      this.snackBar = true
    },
    onLogin() {
      this.loggedIn = true
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 3000);
    },
    tryLogin(payload) {
      console.log(payload)
      if (payload) {
        this.callSnackBar("Logged In", "success")
        this.onLogin()
      }
      if (!payload) this.callSnackBar("Invalid Login", "error")
    },
    sendReset() {
      this.callSnackBar("Reset Link Sent", "blue")
    }
  }
}
</script>
