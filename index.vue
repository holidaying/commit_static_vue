<template>
    <div class="js-calendar-graph">
        <svg
            width="828"
            height="128"
            class="js-calendar-graph-svg"
            id="calendarGraph"
        >
            <g transform="translate(10, 20)">
                <g
                    :transform="'translate(' + (index * 16 + 50) + ', 0)'"
                    v-for="(item, index) in list"
                    :key="index"
                    :data-day="item.day"
                >
                    <rect
                        class="day"
                        width="11"
                        height="11"
                        x="16"
                        :y="sindex*15"
                        :fill="(sindex+index)%20==0?'green':'grey'"
                        data-count="0"
                        :data-date="'2019-09-22 '+sitem[sindex]"
                        v-for="(sitem, sindex) in item.hour"
                        :key="sindex"
                    ></rect>
                </g>
                <text text-anchor="start" class="wday" dx="-10" :dy="8+17*index" v-for="(item,index) in yTime" :key="index">{{item}}</text>
            </g>
        </svg>
    </div>
</template>
<script>
import Sunset from "../../apps/vias-hd-front-base/src/components/tree/sunset";
export default {
    data() {
        return {
            list: [],
            yTime:["00:00-02:00", "02:00-04:00", "04:00-06:00", "06:00-08:00","10:00-12:00"]
        };
    },
    mounted() {
        let today = new Date().getDay(),
            firstDay = new Date().getTime() - (today - 1) * 24 * 60 * 1000;
        for (var i = 1; i < 50; i++) {
            this.list.push({
                day: Sunset.Dates.format(
                    firstDay + 24 * 60 * 100 * i,
                    "yyyy-MM-dd"
                ),
                hour: this.yTime
            });
        }
    },
    methods: {
        fillTable() {}
    }
};
</script>
<style lang="less" scoped>
.day:hover{
    opacity: 0.5;
}
</style>
