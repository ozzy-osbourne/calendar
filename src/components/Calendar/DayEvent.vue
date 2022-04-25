<template>

  <div class="event" v-bind:class="[ event.type ]">
    {{getEventTime(event.date)}}
    {{event.name}}
  </div>

</template>

<script>
import moment from 'moment'

export default {
  name: 'DayEvent',
  props: ['event'],
  methods : {
    getEventTime(time) {
      return moment.unix(time).format('HH:mm')
    }
  }
}
</script>

<style scoped>
.event {
  width: 85%;
  padding: 3px 7px;
  border-radius: 5px;
  margin-left: 7px;
  margin-bottom: 5px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.event:hover {
  width: fit-content;
  cursor: pointer;
  position: relative;
}
.green {
  color: #8dc39c;
  background: #ebf8ee;
}
.orange {
  color: #eac092;
  background: #f9ecd9;
}
.red {
  color: #d65a72;
  background: #fceced;
}
</style>
