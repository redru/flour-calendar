<template>
  <div id="app" style="display: flex; justify-content: center;">
    <div style="max-width: 80%;">
      <FlourCalendar :groups="groups"
                     :events="events"
      ></FlourCalendar>
    </div>
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
    mounted: function() {
      this.events = [{
        id: 1,
        room: { id: 1 },
        customer: { name: 'Test Event' },
        checkinDate: moment().hours(8).minutes(0).seconds(0).format(),
        checkoutDate: moment().add(5, 'days').hours(16).minutes(0).seconds(0).format()
      }];
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
        },{
          id: 10,
          name: 'Group 9'
        },{
          id: 11,
          name: 'Group 9'
        },{
          id: 12,
          name: 'Group 9'
        },{
          id: 13,
          name: 'Group 9'
        },{
          id: 14,
          name: 'Group 9'
        },{
          id: 15,
          name: 'Group 9'
        },{
          id: 16,
          name: 'Group 9'
        },{
          id: 17,
          name: 'Group 9'
        },{
          id: 18,
          name: 'Group 9'
        },{
          id: 19,
          name: 'Group 9'
        },{
          id: 20,
          name: 'Group 9'
        },{
          id: 21,
          name: 'Group 9'
        },{
          id: 22,
          name: 'Group 9'
        },{
          id: 23,
          name: 'Group 9'
        },{
          id: 24,
          name: 'Group 9'
        },{
          id: 25,
          name: 'Group 9'
        },{
          id: 26,
          name: 'Group 9'
        },{
          id: 27,
          name: 'Group 9'
        },{
          id: 28,
          name: 'Group 9'
        },{
          id: 29,
          name: 'Group 9'
        }],
        events: []
      }
    }
  }
</script>

<style lang="stylus">

</style>
