<template>
  <div class="dragDemo">
    <!--列表1-->
    <draggable
      class="list-group"
      element="div"
      v-model="listLeft"
      :options="dragOptions1"
      :move="onMove"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <div v-for="(item, key) in listLeft" :key="key">
        <img src="http://oss.shangmian.xin/ciBm3U1544694909000?imageslim" />
        {{ item.name }}-{{ item.value }}
      </div>
    </draggable>
    <!--列表2-->
    <draggable
      class="list-group"
      element="div"
      v-model="listRight"
      :options="dragOptions1"
      :move="onMove"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <div v-for="(item, key) in listRight" :key="key">
        <img src="http://oss.shangmian.xin/ciBm3U1544694909000?imageslim" />
        {{ item.name }}-{{ item.value }}
      </div>
    </draggable>
    <!--列表3-->
    <draggable
      class="list-group"
      element="div"
      v-model="listThree"
      :options="dragOptions1"
      :move="onMove"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <div v-for="(item, key) in listThree" :key="key">
        <img src="http://oss.shangmian.xin/ciBm3U1544694909000?imageslim" />
        {{ item.name }}-{{ item.value }}
      </div>
    </draggable>
    <!-- <div v-for="(value, key, index) in dayTable" :key="index">
      <draggable
        v-for="(lValue, lKey, lIndex) in value"
        :key="lIndex"
        class="list-group"
        element="div"
        :model="lValue"
        :options="dragOptions1"
        :move="onMove"
        @start="isDragging = true"
        @end="isDragging = false"
      >
        <div v-for="(item, key) in lValue" :key="key">
          <img src="http://oss.shangmian.xin/ciBm3U1544694909000?imageslim" />
          {{ item.name }}-{{ item.value }}
        </div>
      </draggable>
    </div> -->
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "dragDemo",
  components: {
    draggable
  },
  data() {
    return {
      isDragging: false,
      listLeft: [
        {
          name: "数据一",
          value: "1"
        },
        {
          name: "数据二",
          value: "2"
        },
        {
          name: "数据三",
          value: "3"
        },
        {
          name: "数据四",
          value: "4"
        },
        {
          name: "数据五",
          value: "5"
        }
      ],
      listRight: [],
      listThree: [],
      dayTable: {
        mon: {},
        tue: {},
        wed: {},
        thur: {},
        fri: {},
        sat: {},
        sun: {}
      }
    };
  },
  created() {
    this.setDayTable();
  },
  computed: {
    dragOptions1() {
      return {
        animation: 0,
        group: {
          name: "description"
        },
        ghostClass: "ghost"
      };
    },
    dragOptions2() {
      return {
        animation: 0,
        group: {
          name: "description",
          pull: "clone",
          put: false
        },
        group: "description"
      };
    },
    dragOptions3() {
      return {
        animation: 0,
        group: {
          name: "description",
          pull: "clone",
          put: false
        },
        group: "description"
      };
    }
  },
  methods: {
    setDayTable() {
      const oMinute = 14 * 60;
      // console.log(oMinute)
      Object.keys(this.dayTable).map(item => {
        console.log(oMinute / 30);
        for (let i = 0; i < oMinute / 30; i++) {
          // this.dayTable[item].push({
          //   time: (Array(2).join(0) + String((7 * 60 + i * 30) / 60).split('.')[0]).slice(-2)
          // })
          this.dayTable[item][
            `${(
              Array(2).join(0) + String((7 * 60 + i * 30) / 60).split(".")[0]
            ).slice(-2)}:${(
              Array(2).join(0) + String((7 * 60 + i * 30) % 60).split(".")[0]
            ).slice(-2)}`
          ] = [];
        }
        // console.log(this.dayTable[item])
      });
      console.log(this.dayTable);
    },
    onMove({ relatedContext, draggedContext }) {
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      console.log(relatedContext, draggedContext);
      return (
        (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      );
    }
  }
};
</script>

<style scoped lang="scss" rel="stylesheet/scss">
.dragDemo {
  margin-top: 50px;
  display: flex;
  justify-content: center;
  color: #555;
  .list-group {
    width: 300px;
    border: 1px solid #ddd;
    text-align: center;
    margin-right: 50px;
    > div {
      padding: 10px;
      border-bottom: 1px dashed #ddd;
      img {
        width: 25px;
        height: 25px;
        vertical-align: middle;
        padding-right: 10px;
      }
    }
  }
}
</style>
