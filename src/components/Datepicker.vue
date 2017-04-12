
<style>
    .datepicker__container {
        position:relative;
    }
</style>
<template>
    <div>
        <div class="datepicker__container">
            <input type='text' :value='date_formatted' @click="showDatePicker"/>

            <datepicker-agenda :date='date' @change="selectDate" @cancel="hideDatePicker" :visible="isVisible"></datepicker-agenda>
        </div>
    </div>

</template>

<script>
import moment from 'moment'
moment.locale('fr')

import DatePickerAgenda from './DatepickerAgenda.vue'

export default {
  props: {
    value: {type: String, required: true},
    format: {type: String, default: 'YYYY-MM-DD'}
  },
  components: {
    'datepicker-agenda': DatePickerAgenda
  },
  data () {
    return {
      isVisible: false,
      date: moment(this.value, 'YYYY-MM-DD')
    }
  },
  methods:{
    selectDate (date) {
        this.date = date;
        this.hideDatePicker();
    },
    showDatePicker () {
        this.isVisible = true;
       setTimeout(() => document.addEventListener("click",this.hideDatePicker),0);
    },
    hideDatePicker () {
        this.isVisible = false;
        document.removeEventListener("click", this.hideDatePicker);
    }
  },
  computed: {
    date_formatted () {
      return this.date.format(this.format)
    }
  },
  template: `
`
}
</script>
