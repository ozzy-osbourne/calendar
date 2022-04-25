<template>
  <div class="cell-wrapper" v-bind:class="[ { 'past-day': isPastDay, 'current-day': isCurrentDay } ]">
      
      <div class="day-wrapper">
        <div class="day" v-bind:class="[ { 'weekend': isWeekend } ]">
          {{dayItem.format('D')}}
        </div>
      </div>

      <div>
        <DayEvent
          v-for="event in todayEvents" :key="event.id"
          :event="event"
        ></DayEvent>
      </div>

  </div>
</template>

<script>
import DayEvent from './DayEvent.vue'
import moment from 'moment'

export default {
  name: 'CalendarDay',
  props: ['dayItem', 'events'],
  components: {
    DayEvent
  },
  computed:{
    isCurrentDay() {
      return moment().isSame(this.dayItem, 'day');
    },
    isPastDay() {
      return this.dayItem < moment().subtract(1, 'day');
    },
    isWeekend() {
      return this.dayItem.day() === 6 || this.dayItem.day() === 0;
    },
    todayEvents() {
      return this.events.filter(event => event.date >= this.dayItem.format('X') && event.date <= this.dayItem.clone().endOf('day').format('X') );
    }
  }
}
</script>

<style scoped>
.cell-wrapper {
  border-radius: 10px;
  min-width: 148px;
  min-height: 88px;
  border: 1px solid #f5f5f5;
  color: #383838;

  display: flex;
  flex-direction: column;
}
.day-wrapper {
  display: flex;
  justify-content: flex-end; 
}
.day {
  width: 33px;
  height: 33px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}
.weekend {
  color: #a1a8d1;
}
.current-day {
  border: 1px solid #a6a6a6;
}
.current-day .day-wrapper .day {
  color: #8dc39c;
}
.past-day {
  background: #f5f5f5;
}
</style>
