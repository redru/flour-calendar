<template>
    <div class="cal-container">
        <!-- TOOLBAR -->
        <Toolbar :current-date="currentDate"
                 :target-date="targetDate"
                 @on-next="changeDate('next')"
                 @on-back="changeDate('back')"
        ></Toolbar>

        <!-- CONTENT -->
        <div class="cal-scroller"
             @mouseleave="currentResource = null; selectedDatetime = null;">

            <!-- HEADERS -->
            <Headers :date-length="DATE_LENGTH"
                     :time-box-length="TIME_BOX_LENGTH"
                     :time-box-height="TIME_BOX_HEIGHT"
                     :dateHeaders="dateHeaders"
                     :sections="sections"
                     :selectedDateTime="selectedDatetime"></Headers>
            <!-- DATA  -->
            <div v-for="resource in resources" :key="'r:' + resource.id"
                 style="display: flex;">
                <!-- CELLS -->
                <div style="flex: 0 0 130px; position: sticky; left: 0; z-index: 888; height: 50px; line-height: 50px;">
                    <span>{{resource.name}}</span>
                </div>

                <div style="flex: 0 0 20px;"></div>

                <div style="flex: 1; display: flex;">
                    <div v-for="section in sections" :key="'s:' + section.id"
                         @mouseover="currentResource = resource.id; selectedDatetime = section.dateTime;"
                         :id="resource.id + ':' + section.dateTime"
                         class="data-row  "
                         style="flex: 0 0 80px; height: 50px; line-height: 50px; ">
                    </div>
                </div>
            </div>

            <!-- EVENTS -->
            <Event v-for="event in parsedEventsList" :key="event.id"
                   :style="{'background-color': 'steelblue', 'border-radius': '10px', 'color': 'white'}"
                   :text="event.title"
                   :positioning="event.positioning"
            ></Event>
        </div>
    </div>
</template>

<script>
    import '@fortawesome/fontawesome-free/css/all.css';
    
    import moment from 'moment';
    import Event from './Event';
    import Headers from './Headers';
    import Toolbar from './Toolbar';

    export default {
        props: {
            events: Array,
            groups: Array
        },
        components: {
            Event,
            Headers,
            Toolbar
        },
        created: function() {
            // this.loadHeaders(this.currentDate);
        },
        data: function() {
            const TIME_STEP = 4;
            const PERIOD_LENGTH = 16;
            const currentDate = moment().hours(0).minutes(0).seconds(0);

            return {
                // Constants
                TIME_STEP: TIME_STEP,
                DATE_LENGTH: 24 / TIME_STEP,
                TIME_BOX_LENGTH: 80,
                TIME_BOX_HEIGHT: 25,
                PERIOD_LENGTH: PERIOD_LENGTH,
                // Calendar configuration
                currentDate: currentDate,
                targetDate: currentDate.clone().add(PERIOD_LENGTH, 'days'),
                sectionGroups: [],
                resources: this.groups,
                // States
                currentResource: null,
                selectedDatetime: null
            }
        },
        methods: {
            changeDate: function(newDate) {
                alert(newDate);
                // this.loadHeaders(newDate);
            }
        },
        computed: {
            sections: function() {
                const startDate = this.currentDate.clone();
                const endDate = startDate.clone().add(this.PERIOD_LENGTH, 'days');

                const sectionsList = [];

                while (startDate < endDate) {
                    sectionsList.push({
                        id: startDate.format(),
                        hours: startDate.hours(),
                        minutes: startDate.minutes(),
                        date: startDate.format('DD-MMM-YYYY'),
                        dateTime: startDate.format()
                    });

                    startDate.add(this.TIME_STEP, 'hours');
                }

                return sectionsList;
            },
            dateHeaders: function() {
                const headers = [];

                for (let currentDate = this.currentDate.clone(); currentDate < this.targetDate; currentDate.add(1, 'day')) {
                    headers.push({ date: currentDate.format('DD MMM YYYY') })
                }

                return headers;
            },
            parsedEventsList: function() {
                const parsedEvents = [];

                /* const startDate = this.currentDate.clone();
                const endDate = startDate.clone().add(this.PERIOD_LENGTH, 'days');

                for (let event of this.events) {
                    let eventCheckin = moment.utc(event.checkinDate).local();
                    let eventCheckout = moment.utc(event.checkoutDate).local();

                    if (eventCheckin < startDate) {
                        eventCheckin = startDate.clone();
                    }

                    if (eventCheckout > endDate) {
                        eventCheckout = endDate.clone();
                    }

                    const difference = moment.duration(eventCheckout.diff(eventCheckin)).asHours();

                    const elementStart = document.getElementById(event.room.id + ':' + eventCheckin.format());

                    parsedEvents.push({
                        id: event.id,
                        checkinDate: eventCheckin,
                        checkoutDate: eventCheckout,
                        title: event.customer.name,
                        positioning: {
                            x: elementStart.offsetLeft + 'px',
                            y: (elementStart.offsetTop + this.TIME_BOX_HEIGHT / 2) + 'px',
                            width: (difference / this.TIME_STEP * this.TIME_BOX_LENGTH) + 'px',
                            height: this.TIME_BOX_HEIGHT + 'px'
                        }
                    });
                }*/

                return parsedEvents;
            }
        }
    }
</script>

<style lang="stylus">
    .cal-container
        max-height 100%
        max-width 100%

    .cal-scroller
        max-height 100%
        overflow-x auto
        overflow-y auto
        position relative

    .cal-scroller::-webkit-scrollbar
        width 0 !important

    .data-row
        // border 1px solid lightgrey
        box-shadow 0 0 0 0 rgba(0,0,0,0)
        transition 0.15s

    .data-row:hover
        box-shadow 0 0 8px 0 rgba(0,0,0,0.2)

    .current-active
        box-shadow 0 0 8px 0 rgba(0,0,0,0.2)

    .first-row
        border-top dodgerblue 1px solid
</style>
