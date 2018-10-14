<template>
  <v-container fluid grid-list-md>
    <v-layout align-center justify-space-around row>
      <v-flex xs12 sm8 md8 mt-5>
        <v-menu ref="menu" :close-on-content-click="false" v-model="menu" :nudge-right="40" lazy transition="scale-transition" offset-y full-width min-width="290px">
          <v-text-field slot="activator" v-model="date" solo label="Date of Birth" prepend-icon="event" readonly></v-text-field>
          <v-date-picker ref="picker" v-model="date" :max="new Date().toISOString().substr(0, 10)" min="1950-01-01" @change="save"></v-date-picker>
        </v-menu>
        &emsp;
        <v-menu ref="menu1" :close-on-content-click="false" v-model="menu1" :nudge-right="40" lazy transition="scale-transition" offset-y full-width min-width="290px">
          <v-text-field slot="activator" v-model="date1" solo label="Age at the date of" prepend-icon="event" readonly></v-text-field>
          <v-date-picker ref="picker" v-model="date1" min="1950-01-01" @change="save1"></v-date-picker>
        </v-menu>
      </v-flex>
    </v-layout>
    <v-btn :disabled="!disabled" @click="calculateDate">Find out</v-btn>
    <span v-if="diffDays" class="days">
      <div>
        Age: {{years}}
      </div>
      <div>
        Total Days: {{diffDays}}
      </div>
      <div>
        Total Weeks: {{weeksBetween}}
      </div>
    </span>

  </v-container>
</template>

<script>
  export default {
    data: () => ({
      date: null,
      menu: false,
      menu1: false,
      date1: null,
      diffDays: null,
      years: null,
      weeksBetween: null
    }),
    watch: {
      menu(val) {
        val && this.$nextTick(() => (this.$refs.picker.activePicker = 'YEAR'));
      }
    },
    methods: {
      save(date) {
        this.$refs.menu.save(date);
      },
      save1(date) {
        this.$refs.menu1.save(date);
      },
      calculateDate() {
        let fdate = new Date(this.date);
        let ldate = new Date(this.date1);
        let timeDiff = Math.abs(ldate.getTime() - fdate.getTime());
        this.diffDays = Math.ceil(timeDiff / (1000 * 3600 * 24));
        let diffDate = new Date(ldate - fdate);
        this.years =
          diffDate.toISOString().slice(0, 4) -
          1970 +
          ' Years, ' +
          diffDate.getMonth() +
          ' Months, ' +
          (diffDate.getDate() - 1) +
          ' Days ';
        this.weeksBetween = Math.round(
          (ldate - fdate) / (7 * 24 * 60 * 60 * 1000)
        );
      }
    },
    computed: {
      disabled() {
        if (this.date && this.date1) {
          return true;
        } else {
          return false;
        }
      }
    }
  };
</script>

<style>
  .days {
    color: white;
    font-size: 30px;
  }
  .days > div {
    margin-top: 3%;
  }
  .theme--light.v-icon {
    color: white !important;
  }
</style>
