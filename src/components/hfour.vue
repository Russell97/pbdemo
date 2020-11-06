<template>
  <div class="fullCalendarCont" style="display: flex; justify-content: space-between;">
    <div style="width: 30%; background #ccc;">
      <div class="box box-solid">
        <div class="box-header with-border">
          <h4 class="box-title">Draggable Events</h4>
        </div>
        <div class="box-body">
          <!-- the events -->
          <div id="external-events">
            <!-- ccrq改动1:给每个添加一个img标签  这些图片位置在 pages 目录下 -->
            <div class="external-event bg-green">
              Lunch
            </div>
            <div class="external-event bg-yellow">
              Go home
            </div>
            <div class="external-event bg-aqua">
              Do homework
            </div>
            <div class="external-event bg-light-blue">
              Work on UI design
            </div>
            <div class="external-event bg-red">
              Sleep tight
            </div>
            <!-- ccrq改动1:  结束  -->
            <div class="checkbox">
              <label for="drop-remove">
                <input type="checkbox" id="drop-remove" />
                remove after drop
              </label>
            </div>
          </div>
        </div>
        <!-- /.box-body -->
      </div>
      <!-- /. box -->
      <div class="box box-solid">
        <div class="box-header with-border">
          <h3 class="box-title">Create Event</h3>
        </div>
        <div class="box-body">
          <div class="btn-group" style="width: 100%; margin-bottom: 10px;">
            <!--<button type="button" id="color-chooser-btn" class="btn btn-info btn-block dropdown-toggle" data-toggle="dropdown">Color <span class="caret"></span></button>-->
            <ul class="fc-color-picker" id="color-chooser">
              <li>
                <a class="text-aqua" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-blue" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-light-blue" href="#"
                  ><i class="fa fa-square"></i
                ></a>
              </li>
              <li>
                <a class="text-teal" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-yellow" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-orange" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-green" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-lime" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-red" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-purple" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-fuchsia" href="#"
                  ><i class="fa fa-square"></i
                ></a>
              </li>
              <li>
                <a class="text-muted" href="#"><i class="fa fa-square"></i></a>
              </li>
              <li>
                <a class="text-navy" href="#"><i class="fa fa-square"></i></a>
              </li>
            </ul>
          </div>
          <!-- /btn-group -->
          <div class="input-group">
            <input
              id="new-event"
              type="text"
              class="form-control"
              placeholder="Event Title"
            />

            <div class="input-group-btn">
              <button
                id="add-new-event"
                type="button"
                class="btn btn-primary btn-flat"
              >
                Add
              </button>
            </div>
            <!-- /btn-group -->
          </div>
          <!-- /input-group -->
        </div>
      </div>
    </div>
    <full-calendar
      style="flex: 1; background #000;"
      :config="config"
      :events="events"
      ref="calendar"
    ></full-calendar>
  </div>
</template>
<script>
import { FullCalendar } from "vue-full-calendar";
import "fullcalendar/dist/fullcalendar.css";
export default {
  components: { FullCalendar },
  data() {
    return {
      selectDate: "", //日期选择器选中的月份
      events: [
        {
          id: 1,
          title: "出差",
          start: "2020-07-20", // 事件开始时间
          end: "2020-07-21" // 事件结束时间
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
        selectable: true, //是否允许用户单击或者拖拽日历中的天和时间隙
        eventLimit: false, // 限制一天中显示的事件数，默认false
        allDaySlot: true, //是否显示allDay
        displayEventEnd: true, //是否显示结束时间
        allDayText: "全天",
        navLinks: true, //允许天/周名称是否可点击
        defaultView: "agendaWeek", //显示默认视图
        eventClick: this.eventClick, //点击事件
        dayClick: this.dayClick, //点击日程表上面某一天
        eventRender: this.eventRender
      }
    };
  },
  watch: {
    events: {
      handler: function(newVal, oldVal) {
        //do something
        console.log("++++++++++++++++++");
        console.log(newVal);
      },
      deep: true
    }
  },
  mounted() {
    let date = {};
    let weekOfday = parseInt(this.$moment().format("d")); // 计算今天是这周第几天 周日为一周中的第一天
    let start = this.$moment()
      .subtract(weekOfday - 1, "days")
      .format("YYYY-MM-DD"); // 周一日期
    let end = this.$moment()
      .add(7 - weekOfday, "days")
      .format("YYYY-MM-DD"); // 周日日期
    for (let i = 0; i < 7; i++) {
      date[i] = this.$moment()
        .subtract(weekOfday - i, "days")
        .format("YYYY-MM-DD");
    }
    this.events.map(item => {
      if (item.start) {
        const startArr = item.start.split(" ");
        startArr[0] = date[parseInt(this.$moment(startArr[0]).format("d"))];
        item.start = startArr.join(" ");
      }
      if (item.end) {
        const endArr = item.end.split(" ");
        endArr[0] = date[parseInt(this.$moment(endArr[0]).format("d"))];
        item.end = endArr.join(" ");
      }
    });
  },
  methods: {
    demo() {
      console.log(this.events);
    },
    changeDate() {
      console.log(this.selectDate)
      this.$refs.calendar.fireMethod("gotoDate", this.selectDate);
    },
    // 点击事件
    eventClick(event, jsEvent, pos) {
      console.log("eventClick", event, jsEvent, pos);
    },
    // 点击当天
    dayClick(day, jsEvent) {
      console.log("dayClick", day, jsEvent);
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
