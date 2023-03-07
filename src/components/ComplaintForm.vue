<template>
  <div>
    <input v-model="flightNumber" id="flight-number" class="form-control" :class="flightNumberValid(flightNumber) ? 'is-valid' : 'is-invalid'">
    <input v-model="emailAddress" id="email-address" class="form-control" :class="emailAddressValid(emailAddress) ? 'is-valid' : 'is-invalid'">
    <input v-model="flightDate" id="flight-date" class="form-control" :class="dateValid(flightDate) ? 'is-valid' : 'is-invalid'">
    <input v-model="flightTime" id="flight-time" class="form-control" :class="timeValid(flightTime) ? 'is-valid' : 'is-invalid'">
    <input v-model="bankIban" id="bank-iban" class="form-control" :class="ibanValid(bankIban) ? 'is-valid' : 'is-invalid'">
  </div>
  <img src='@/assets/overview.jpg' class='img-fluid rounded' alt=''>
</template>

<script>

export default {
  name: 'ComplaintForm',
  data() {
    return {
      formSubmitted: false,
      flightNumber: '',
      emailAddress: '',
      flightDate: '',
      flightTime: '',
      bankIban: '',
      flightNumberRe: /^([A-Z]{2}|[A-Z]\d|\d[A-Z])(\s?)(\d{0,4})$/,
      emailAddressRe: /(^\w[a-z0-9._%+-]+)@(tu-berlin.de|mailbox.tu-berlin.de|campus.tu-berlin.de)$/,
      dateRe: /^(\d{1,4})-(0[1-9]|[1-9]|1[0-2])-([1-9]|0[1-9]|1[0-9]|2[0-9]|3[0-1])$/,
      timeRe: /^([0-9]|[0-1][0-9]|2[0-3]):([0-5][0-9])$/,
      ibanRe: /^DE\d{2}\s?\d{4}\s?\d{4}\s?\d{4}\s?\d{4}\s?\d{2}$/
    };
  },
  methods: {
    flightNumberValid(value) {
      return (this.flightNumberRe.test(value) && this.formSubmitted);
    },
    emailAddressValid(value) {
      return (this.emailAddressRe.test(value) && this.formSubmitted);
    },
    dateValid(value) {
      return (this.dateRe.test(value) && this.formSubmitted);
    },
    timeValid(value) {
      return (this.timeRe.test(value) && this.formSubmitted);
    },
    ibanValid(value) {
      let num = 0;
      let val = value.replaceAll(" ", "");
      for(let i = 4; i < val.length; i++){
          num += parseInt(val[i]);
      }
      let st = value.substring(2, 4);
      return (this.ibanRe.test(value) && this.formSubmitted && num == st);
    },
  }
}
</script>

<style scoped>
#main-card {
  background-color: rgba(255, 255, 255, 0.9);
}
</style>