<template>
  <v-app dark >
    <v-main >
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer class="d-flex align-center justify-center py-2" style="background-color: #121212;">
      <div class="d-flex flex-column align-center">
        <p class="text-caption my-0">Defcon OS &copy; 2022</p>
        <p class="text-caption mb-0 mt-1">Powered By Arch Linux</p>
      </div>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>
