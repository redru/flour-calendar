<template>
    <div class="cal-toolbar" style="display: flex;">
        <div class="toolbar-side left" style="flex: 0 0 130px; display: flex;">
            <div class="toolbar-item" @click="$emit('on-back')">
                <i class="fas fa-angle-left"></i>
            </div>
            <div class="toolbar-item">
                <i class="far fa-calendar-alt"></i>
            </div>
            <div class="toolbar-item" @click="$emit('on-next')">
                <i class="fas fa-angle-right"></i>
            </div>
        </div>

        <div style="flex: 0 0 20px;"></div>

        <div class="toolbar-side right" style="flex: 1;display: flex;">
            <span>{{currentDate.format('DD MMM YYYY')}}</span>
            <span>{{targetDate.format('DD MMM YYYY')}}</span>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            currentDate: Object,
            targetDate: Object
        }
    }
</script>

<style lang="stylus">
    .cal-toolbar
        font-size larger
        font-weight bolder
        padding 1vw

    .cal-toolbar .toolbar-side
        justify-content space-between

    .cal-toolbar .toolbar-side .toolbar-item
        cursor pointer
</style>
