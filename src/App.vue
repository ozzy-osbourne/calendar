<template>
  <div id="app">
    
    <VueCalendar :events="events"></VueCalendar>
    
  </div>
</template>

<script>
import VueCalendar from './components/Calendar/VueCalendar.vue'

export default {
  name: 'App',
  components: {
    VueCalendar
  },
  data () {
    return {
      events: [
        {
          id: 1,
          name: 'Купить очень много хлеба',
          date: 1649929145,
          type: 'red',
        },
        {
          id: 2,
          name: 'Купить колбасу',
          date: 1649938865,
          type: 'green',
        },
        {
          id: 3,
          name: 'Купить молоко',
          date: 1650748865,
          type: 'orange',
        },
        {
          id: 4,
          name: 'Купить масло',
          date: 1648633145,
          type: 'green',
        },
        {
          id: 5,
          name: 'Сходить по делам',
          date: 1646645945,
          type: 'green',
        },
        {
          id: 6,
          name: 'Отпраздновать день победы',
          date: 1652089145,
          type: 'green',
        },
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  /* color: #2c3e50; */
}
</style>
