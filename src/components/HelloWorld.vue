<template>
<div>
  <div>
    <h1>Lotte Bike Parking Report</h1>
  </div>
  <div>
    <form class="md-layout md-alignment-top-center">
      <md-card class="md-layout-item md-size-50 md-small-size-100">
        <md-card-content>
          <div class="md-layout md-gutter">
            <div class="md-layout-item md-small-size-100">
              <md-field>
                <label>Name</label>
                <md-input v-model="name"></md-input>
              </md-field>
            </div>
          </div>
          <div class="md-layout md-gutter">
            <div class="md-layout-item md-small-size-100">
              <md-field>
                <label>Amount</label>
                <md-input v-model="amount"></md-input>
              </md-field>
            </div>
          </div>
          <div class="md-layout md-gutter">
            <div class="md-layout-item md-small-size-100">
              <md-datepicker v-model="startDate">
                <label>Start date</label>
              </md-datepicker>
            </div>
          </div>
          <div class="md-layout md-gutter">
            <div class="md-layout-item md-small-size-100">
              <md-datepicker v-model="endDate">
                <label>End date</label>
              </md-datepicker>
            </div>
          </div>
          <md-card-actions>
            <md-button type="button" class="md-raised md-primary" v-on:click.stop="onSubmit">Create Report</md-button>
          </md-card-actions>
        </md-card-content>
      </md-card>
    </form>
  </div>
</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
  name: 'bikeParkingReport',
  data: () => ({
    name: undefined,
    amount: undefined,
    startDate: undefined,
    endDate: undefined
  }),
  methods: {
    onSubmit() {
      if (this.name === undefined || this.amount === undefined || this.startDate === undefined || this.endDate === undefined) {
        return;
      }
      const start = moment(this.startDate.toString())
      const end = moment(this.endDate.toString())

      if(start.unix() >= end.unix()) return;

      axios.post('/bikepark', {
        name: this.name,
        amount: this.amount,
        startDate: start,
        endDate: end
      }).then(() => {
        window.location.href = '/Theo doi gui xe_HN_' + this.name + '.xlsx'
      })
    }
  }
}
</script>
