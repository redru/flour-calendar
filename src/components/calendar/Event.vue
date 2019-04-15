<template>
    <div class="calendar-event"
         :style="{'top': positioning.y, 'left': positioning.x, 'width': positioning.width, 'height': positioning.height}">
        <span>{{eventText}}</span>
    </div>
</template>

<script>
    // import moment from 'moment';

    export default {
        props: {
            positioning: Object,
            text: String
        },
        mounted: function() {
        },
        data: function() {
            return {
                eventPositioning: this.positioning,
                eventText: this.text
            }
        }
    }
</script>

<style lang="stylus">
    .calendar-event
        background-color forestgreen
        position absolute
</style>
