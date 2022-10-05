<template>
  <v-card>
    <v-divider dark />
    <v-card-text>
      <v-container class="pa-0" fluid>
        <v-row>
          <v-col cols="6">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;">GPUs</v-chip>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-chip color="success" style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" v-if="!loading">1 On</v-chip>
            <v-progress-circular
              indeterminate
              color="accent"
              v-else
            ></v-progress-circular>
          </v-col>
        </v-row>
        <v-divider dark class="my-4" />
        <v-row>
          <v-col cols="6">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;">F2pool</v-chip>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" v-if="!loading">172 MH/s</v-chip>
            <v-progress-circular
              indeterminate
              color="accent"
              v-else
            ></v-progress-circular>
          </v-col>
        </v-row>
        <v-divider dark class="my-4" />
        <v-row>
          <v-col cols="6">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" color="red lighten-2">Cost (24h)</v-chip>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" v-if="!loading">CAD {{ costFormatted }}</v-chip>
            <v-progress-circular
              indeterminate
              color="accent"
              v-else
            ></v-progress-circular>
          </v-col>
        </v-row>
        <v-divider dark class="my-4" />
        <v-row>
          <v-col cols="6">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" color="green darken-1">Profit (24h)</v-chip>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" v-if="!loading">CAD {{ profitFormatted }}</v-chip>
            <v-progress-circular
              indeterminate
              color="accent"
              v-else
            ></v-progress-circular>
          </v-col>
        </v-row>
        <v-divider dark class="my-4" />
        <v-row>
          <v-col cols="6">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" color="green darken-1">Balance</v-chip>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" v-if="!loading">CAD {{ balanceFormatted }}</v-chip>
            <v-progress-circular
              indeterminate
              color="accent"
              v-else
            ></v-progress-circular>
          </v-col>
        </v-row>
        <v-divider dark class="my-4" />
        <v-row>
          <v-col cols="6">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" color="blue">Threshold</v-chip>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-chip style="min-width: 125px; max-width: 130px; display: grid; place-items: center;" v-if="!loading">CAD 375.00</v-chip>
            <v-progress-circular
              indeterminate
              color="accent"
              v-else
            ></v-progress-circular>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-btn color="blue" text dense width="100%" @click="refresh">Refresh</v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-btn color="red" text dense width="100%" @click="dialog = true">Terminate</v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
    <v-dialog
      v-model="dialog"
      style="height: 100%;"
    >
      <v-card>
        <v-card-title>
          <p class="pa-0 ma-0 error--text">
            Warning
          </p>
        </v-card-title>
        <v-card-text>
          Terminate farm permanently?
        </v-card-text>
        <v-card-actions class="d-flex justify-space-between align-center py-2">
          <v-btn
            text
            @click="dialog = false"
          >
            Cancel
          </v-btn>
          <v-btn
            color="error"
            text
            @click="dialog = false"
          >
            Terminate
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      balance: 28.14,
      profit: 1.01,
      cost: 0.75,
      loading: false,
      dialog: false
    }
  },
  computed: {
    balanceFormatted() {
      return this.balance.toFixed(2)
    },
    profitFormatted() {
      return this.profit.toFixed(2)
    },
    costFormatted() {
      return this.cost.toFixed(2)
    }
  },
  methods: {
    refresh() {
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1000);
    }
  }
}
</script>