<template>
    <div class="calendar-event"
         :style="{'top': positioning.y, 'left': positioning.x, 'width': positioning.width, 'height': positioning.height, 'line-height': positioning.height}">
        <span style="position: sticky; left: 0;">{{eventText}}</span>
    </div>
</template>

<script>
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
