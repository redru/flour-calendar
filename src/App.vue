<template>
  <div id="app" style="display: flex; justify-content: center;">
    <FlourCalendar :groups="groups"
                   :events="events"
    ></FlourCalendar>
  </div>
</template>

<script>
  import moment from 'moment';
  import FlourCalendar from './components/calendar/FlourCalendar';

  export default {
    name: 'app',
    components: {
      FlourCalendar
    },
    data: function() {
      return {
        groups: [{
          id: 1,
          name: 'Group 1'
        },{
          id: 2,
          name: 'Group 2'
        },{
          id: 3,
          name: 'Group 3'
        },{
          id: 4,
          name: 'Group 4'
        },{
          id: 5,
          name: 'Group 5'
        },{
          id: 6,
          name: 'Group 6'
        },{
          id: 7,
          name: 'Group 7'
        },{
          id: 8,
          name: 'Group 8'
        },{
          id: 9,
          name: 'Group 9'
        },],
        events: [{
          id: 1,
          room: { id: 1 },
          customer: { name: 'Luca Zenobi' },
          checkinDate: moment().hours(10).minutes(0).seconds(0).format(),
          checkoutDate: moment().add(5, 'days').hours(20).minutes(0).seconds(0).format()
        }]
      }
    }
  }
</script>

<style>
  body {
    margin: 0;
  }

  #app {
    /*width: 80%;*/
  }
</style>
