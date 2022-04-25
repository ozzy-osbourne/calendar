<template>
  <div>
    <button v-on:click="$emit('toggle-date', 'prevMonth')"> &lt; </button>
    <button class="month" v-on:click="$emit('toggle-date', 'currentMonth')">{{currentMonth.format('MMMM')}} {{isCurrentYear}}</button>
    <button v-on:click="$emit('toggle-date', 'nextMonth')"> &gt; </button>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'CalendarHead',
  props: ['currentMonth'],
  computed: {
    isCurrentYear() {
      return moment().format('YYYY') != this.currentMonth.format('YYYY') ? this.currentMonth.format('YYYY') : '';
    }
  }
}
</script>

<style scoped>
span {
  font-size: 32px;
  font-weight: bold;
  margin-right: 8px;
}
div {
  padding: 5px;
}
button {
  border: unset;
  background: none;
  height: 20px;
  font-size: 20px;
  margin-right: 2px;
  font-weight: bold;
  color: #3b4587;
}
.month {
  text-transform: uppercase; 
}
</style>
