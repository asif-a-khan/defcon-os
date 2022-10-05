<template>
  <v-container fluid>
    <v-row no-gutters class="mb-4">
      <v-col cols="12">
        <v-card>
          <v-card-title style="background-color: #272727;" class="d-flex align-center justify-space-between">
            <p class="ma-0">Asif's Grid</p>
            <v-btn color=" blue" dense text @click="logout">Logout</v-btn>
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
    <v-row no-gutters>
      <v-col cols="12">
        <v-container fluid class="px-0">
          <v-tabs v-model="tab" grow>
            <v-tab>Group</v-tab>
            <v-tab>Personal</v-tab>
          </v-tabs>
        </v-container>
      </v-col>
    </v-row>
    <v-skeleton-loader
      v-bind="attrs"
      type="date-picker"
      v-if="loading"
    ></v-skeleton-loader>
    <v-row
      v-if="expand1 && !loading"
    >
      <v-col cols="12">
        <farm-one />
      </v-col>
    </v-row>
    <v-row
      v-if="expand2 && !loading"
    >
      <v-col cols="12">
        <farm-two />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import FarmOne from './FarmOne.vue'
import FarmTwo from './FarmTwo.vue'
export default {
  components: [FarmOne, FarmTwo],
  data() {
    return {
      expand1: true,
      expand2: false,
      tab: 0,
      loading: false
    }
  },
  watch: {
    tab(newVal, oldVal) {
      if (newVal === 0) this.showFarm1()
      if (newVal === 1) this.showFarm2()
    }
  },
  methods: {
    showFarm1() {
      this.expand2 = false
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1500);
      this.expand1 = true
    },
    showFarm2() {
      this.expand1 = false
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1500);
      this.expand2 = true
    },
    logout() {
      window.location.reload()
    }
  },
}
</script>