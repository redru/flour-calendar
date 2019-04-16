<template>
    <div class="cal-headers" style="display: inline-flex; flex-direction: column;">

        <!-- DATE HEADERS -->
        <div style="display: flex;">
            <div style="flex: 1; display: flex;">
                <div v-for="(header, index) in dateHeaders" :key="header.date"
                     class="cal-date-header"
                     :class="{'odd': index % 2 === 0 }"
                     :style="{'flex': '0 0 ' + (dateLength * timeBoxLength) + 'px', 'height': timeBoxHeight + 'px', 'line-height': timeBoxHeight + 'px'}">
                    <span>{{header.date}}</span>
                </div>
            </div>
        </div>

        <!-- TIME HEADERS -->
        <div style="display: flex;">
            <div style="flex: 1; display: flex;">
                <div v-for="section in sections" :key="section.id"
                     class="cal-time-header"
                     :class="{'current-active': section.dateTime === selectedDateTime}"
                     :style="{'flex': '0 0 ' + timeBoxLength + 'px', 'height': timeBoxHeight + 'px', 'line-height': timeBoxHeight + 'px'}">
                    <span style="">{{('0' + section.hours).slice(-2) + ':' + ('0' + section.minutes).slice(-2)}}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            // Structure
            dateLength: Number,
            timeBoxLength: Number,
            timeBoxHeight: Number,
            // Values
            dateHeaders: Array,
            sections: Array,
            selectedDateTime: String
        }
    }
</script>

<style lang="stylus">
    .cal-headers
        position sticky
        top 0
        z-index 999

    .cal-date-header
        background-color steelblue
        color white
        text-align center

    .cal-date-header.odd
        background-color darkcyan

    .cal-time-header
        border-bottom dodgerblue 1px solid
        text-align center

    .current-active
        box-shadow 0 0 8px 0 rgba(0,0,0,0.2)
</style>
