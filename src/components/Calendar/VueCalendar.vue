<template>
  <div class="wrapper">

    <CalendarHead
      :currentMonth="currentMonth"
      v-on:toggle-date="toggleDateHadnler"
    ></CalendarHead>

    <div class="days-wrapper">
      <div class="week-day"
        v-bind:class="[ { weekend: isWeekend(day) } ]"
        v-for="day in weekDays" :key="day.format('d')"
      >
        {{day.format('dddd')}}
      </div>
    </div>

    <div class="grid-wrapper">
      <CalendarDay
        v-for="dayItem in daysArray" :key="dayItem.format('DDMMYYYY')"
        :dayItem="dayItem"
        :events="events"
      ></CalendarDay>
    </div>

  </div>
</template>

<script>
import CalendarHead from './CalendarHead.vue'
import CalendarDay from './CalendarDay.vue'

import moment from 'moment'
moment.updateLocale('en', {week: {dow: 1}})
moment.locale('ru')

export default {
  name: 'VueCalendar',
  components: {
    CalendarHead,
    CalendarDay
  },
  props: ['events'],
  data () {
    return {
      currentMonth: moment(),
      startDay: moment().startOf('month').startOf('week'),
    }
  },
  methods : {
    toggleDateHadnler(eventType) {
      let newCurrentMonth;
      if (eventType == 'prevMonth') newCurrentMonth = this.currentMonth.clone().subtract(1, 'month');
      if (eventType == 'currentMonth') newCurrentMonth = moment().clone();
      if (eventType == 'nextMonth') newCurrentMonth = this.currentMonth.clone().add(1, 'month');

      this.currentMonth = newCurrentMonth;

      let newStartDay = this.currentMonth.clone().startOf('month').startOf('week');
      this.startDay = newStartDay;
    },
    isWeekend(day) {
      return day.day() === 6 || day.day() === 0;
    }
  },
  computed: {
    weekDays() {
      return [...Array(7)].map((val, index) => moment().day(index + 1));
    },
    daysArray() {
      let day = this.startDay.clone().subtract(1, 'day');
      return [...Array(42)].map(() => day.add(1, 'day').clone());
    }
  }
}
</script>

<style scoped>
.wrapper {
  display :grid;
}
.grid-wrapper {
  display: grid;
  grid-gap: 1px;
  grid-template-columns: repeat(7, 1fr);
  grid-template-rows: repeat(6, 1fr);
}
.weekend {
  color: #a2a2a2;
}
.days-wrapper {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
}
.week-day {
  display: flex;
  padding: 10px;
  font-weight: bold;
  text-transform: uppercase;
  justify-content: flex-end;
}
</style>
