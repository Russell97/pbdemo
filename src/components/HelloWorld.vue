<template>
  <div class="fullCalendarCont">
    <!-- <el-date-picker
      size="small"
      style="width: 144px;"
      v-model="selectDate"
      type="date"
      placeholder="选择时间"
      @change="changeDate"
    >
    </el-date-picker> -->
    <el-button @click="demo">123</el-button>
    <div style="margin: 15px 0 15px; width: 500px;">
      <el-input placeholder="请新增内容" v-model="input2">
        <template slot="append">
          <el-button slot="append" @click="test">新增</el-button>
        </template>
      </el-input>
    </div>

    <draggable
      class="list-group"
      element="div"
      v-model="events1"
      :options="dragOptions1"
      :move="onMove"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <div
        ref="sjContainer"
        style="border: 1px solid #ccc; margin-bottom: 15px;"
      >
        <div v-for="(item, index) in events1" :key="index">
          {{ item.title }}
        </div>
      </div>
    </draggable>
    <draggable
      v-model="events"
      class="list-group"
      element="div"
      :options="dragOptions1"
      :move="onMove"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <full-calendar
        :config="config"
        :events="events"
        @event-drop="abc"
        ref="calendar"
      ></full-calendar>
    </draggable>
  </div>
</template>
<script>
import { FullCalendar } from "vue-full-calendar";
import "fullcalendar/dist/fullcalendar.css";
import draggable from "vuedraggable";

export default {
  components: { FullCalendar, draggable },
  data() {
    return {
      isDragging: false,
      input2: "",
      selectDate: "", //日期选择器选中的月份
      events1: [],
      events: [
        {
          start: "09:30",
          end: "10:00",
          id: "_fc1",
          allDay: false,
          week: "5",
          counts: "2",
          color: "#418caf"
        },
        {
          start: "10:00",
          end: "10:30",
          id: "_fc3",
          allDay: false,
          week: "5",
          counts: "2",
          color: "#e28b41"
        },
        {
          start: "10:30",
          end: "11:00",
          id: "_fc5",
          allDay: false,
          week: "5",
          counts: "2",
          color: "#418caf"
        },
        {
          start: "11:00",
          end: "11:30",
          id: "_fc7",
          allDay: false,
          week: "5",
          counts: "2",
          color: "#e28b41"
        },
        {
          start: "11:30",
          end: "12:00",
          id: "_fc9",
          allDay: false,
          week: "5",
          counts: "2",
          color: "#418caf"
        },
        {
          start: "09:00",
          end: "09:30",
          id: "_fc11",
          allDay: false,
          week: "5",
          counts: "2",
          color: "#e28b41"
        }
      ],
      events2: [
        {
          id: 1,
          title: "出差",
          start: "2020-07-20", // 事件开始时间
          end: "2020-07-20" // 事件结束时间
        },
        {
          id: 2,
          title: "春游1",
          start: "2020-07-12 09:00:00",
          end: "2020-07-12 12:00:00"
        },
        {
          id: 3,
          title: "春游2",
          color: "#ffd900",
          start: "2020-07-12 09:00:00",
          end: "2020-07-12 12:00:00"
        },
        {
          id: 4,
          title: "春游3",
          start: "2020-07-26 13:00:00",
          end: "2020-07-26 15:00:00"
        },
        {
          id: 5,
          title: "春游4",
          start: "2020-07-26 15:00:00",
          end: "2020-07-26 16:00:00"
        },
        {
          id: 6,
          title: "123"
        }
      ],
      config: {
        firstDay: "0", //以周日为每周的第一天
        buttonText: { today: "今天", month: "月", week: "周", day: "日" },
        header: { left: "today", center: "prev, title, next" },
        theme: false, //是否允许使用jquery的ui主题
        height: "auto",
        slotLabelFormat: "HH:mm", // axisFormat 'H(:mm)'
        //slotLabelInterval:1,
        views: {
          month: {
            titleFormat: "YYYY年MMM"
          },
          day: {
            titleFormat: "YYYY年MMMDD日 dddd"
          }
        },
        monthNames: [
          "1月",
          "2月",
          "3月",
          "4月",
          "5月",
          "6月",
          "7月",
          "8月",
          "9月",
          "10月",
          "11月",
          "12月"
        ],
        monthNamesShort: [
          "1月",
          "2月",
          "3月",
          "4月",
          "5月",
          "6月",
          "7月",
          "8月",
          "9月",
          "10月",
          "11月",
          "12月"
        ],
        dayNames: [
          "星期日",
          "星期一",
          "星期二",
          "星期三",
          "星期四",
          "星期五",
          "星期六"
        ],
        dayNamesShort: [
          "星期日",
          "星期一",
          "星期二",
          "星期三",
          "星期四",
          "星期五",
          "星期六"
        ],
        slotDuration: "00:30:00",
        minTime: "07:00",
        maxTime: "21:00",
        locale: "zh-cn",
        editable: true, //是否允许修改事件
        selectable: false, //是否允许用户单击或者拖拽日历中的天和时间隙
        eventLimit: false, // 限制一天中显示的事件数，默认false
        allDaySlot: true, //是否显示allDay
        displayEventEnd: true, //是否显示结束时间
        allDayText: "全天",
        navLinks: true, //允许天/周名称是否可点击
        defaultView: "agendaWeek", //显示默认视图
        // eventClick: this.eventClick, //点击事件
        // dayClick: this.dayClick, //点击日程表上面某一天
        eventRender: this.eventRender
      },
      inWeeks: {}
    };
  },
  watch: {
    events: {
      handler: function(newVal) {
        //do something
      },
      deep: true
    }
  },
  mounted() {
    this.date = {};
    let weekOfday = parseInt(this.$moment().format("d")); // 计算今天是这周第几天 周日为一周中的第一天
    let start = this.$moment()
      .subtract(weekOfday - 1, "days")
      .format("YYYY-MM-DD"); // 周一日期
    let end = this.$moment()
      .add(7 - weekOfday, "days")
      .format("YYYY-MM-DD"); // 周日日期
    for (let i = 0; i < 7; i++) {
      this.date[i] = this.$moment()
        .subtract(weekOfday - i, "days")
        .format("YYYY-MM-DD");
    }
    this.events.map(item => {
      if (item.allDay) {
        item.title = item.counts
        item.color = item.color
        item.start = this.date[item.week]
        item.end = null
      } else {
        item.title = item.counts
        item.color = item.color
        item.start = `${this.date[item.week]} ${item.start}`
        item.end = `${this.date[item.week]} ${item.end}`
      }
    });
  },
  computed: {
    dragOptions1() {
      return {
        animation: 0,
        group: {
          name: "description",
          pull: "clone",
          put: true
        },
        group: "description"
      };
    }
  },
  methods: {
    abc(data) {
      this.events.map((item, index) => {
        if (item.id === data.id) {
          console.log(data);
          if (Object.keys(Object(data.start)).length) {
            const time = this.$moment(data.start).utc().format("YYYY-MM-DD HH:mm:ss").split(' ')
            this.$set(
              this.events[index],
              "start",
              time[1] === '00:00:00' ? time[0] : time.join(' ')
            );
            if (time[1] === '00:00:00') {
              this.$set(
                this.events[index],
                "start",
                time[0]
              );
              this.$set(
                this.events[index],
                "allDay",
                true
              );
            } else {
              this.$set(
                this.events[index],
                "start",
                time.join(' ')
              );
              this.$set(
                this.events[index],
                "allDay",
                false
              );
            }
          }
          if (data.end === null) {
            this.$set(
              this.events[index],
              "end",
              this.$moment(data.start).utc().format("YYYY-MM-DD HH:mm:ss").split(' ')[0]
            );
          } else {
            const time = this.$moment(data.end).utc().format("YYYY-MM-DD HH:mm:ss").split(' ')
            this.$set(
              this.events[index],
              "end",
              time[1] === '00:00:00' ? time[0] : time.join(' ')
            );
          }
        }
      });
      // console.log("7", data);
    },
    onMove({ relatedContext, draggedContext }) {
      this.$refs.calendar.demo()
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      return (
        (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      );
    },
    test() {
      const inDay = String(parseInt(this.$moment().format("d")))
      this.events1.push({
        id: Math.floor(Math.random() * (99999 - 9999)) + 9999,
        title: this.input2,
        allDay: true,
        week: inDay,
        counts: this.input2,
        color: "#e28b41",
        start: this.date[inDay],
        start: this.date[inDay],
      });
    },
    demo() {
      console.log(this.events);
    },
    eventRender(event, element) {
      element.find(".fc-title").attr("title", event.title);
    }
  }
};
</script>

<style lang="scss" scoped>
/deep/ .fc-header-toolbar {
  display: none;
}
</style>
