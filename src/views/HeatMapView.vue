<script setup>
import restrictedSections from '@/assets/restricted-sections.json'
import 'echarts/extension/bmap/bmap'
import HeaderBar from '../components/HeaderBar.vue'
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import video1 from '@/assets/traffic1.mp4'
import video2 from '@/assets/traffic2.mp4'
const route = useRoute()
const locationX = ref()
const locationY = ref()
const section = ref(route.query.section)
restrictedSections.forEach((item) => {
  if (item.section === section.value) {
    locationX.value = item.locationX
    locationY.value = item.locationY
  }
})
onMounted(() => {
  var map = new BMap.Map("center-map")
  if (locationX.value !== undefined && locationY.value !== undefined) {
    map.centerAndZoom(new BMap.Point(locationX.value, locationY.value), 17)
  }
  else {
    map.centerAndZoom(new BMap.Point(120.171387, 30.249298), 17)
  }
  var traffic = new BMap.TrafficLayer()
  map.addTileLayer(traffic)
  map.enableScrollWheelZoom(true)
})

const option = ref({
  title: {
    text: "车流量变化趋势",
    textStyle: {
      color: "#fff",
      fontSize: 22.5,
      fontWeight: 500,
    },
    left: "center",
    top: 5,
  },
  xAxis: {
    type: 'category',
    name: "时间/h",
    data: ['0', '2', '4', '6', '8', '10', '12', '14', '16', '18', '20', '22'],
    axisTick: {
      show: false, // 隐藏刻度线
    },
    axisLabel: {
      color: "#fff",
    },
    axisLine: {
      show: false, // 隐藏坐标轴线
    },
    nameTextStyle: {
      color: "#fff",
    },
  },
  yAxis: {
    type: 'value',
    name: "车流量/百万",
    data: [0, 1, 2, 3, 4, 5, 6],
    axisLabel: {
      color: "#fff",
    },
    nameTextStyle: {
      color: "#fff",
    },
  },
  series: [
    {
      type: 'line',
      smooth: true,
      data: [4, 3, 2, 2.5, 4, 5, 4, 3.5, 4, 2, 4, 1],
      color: "red",
    },
  ],
  grid: {
    top: '30%',
    right: 60,
    bottom: '10%',
  }
});


const option1 = ref({
  title: {
    text: "车辆状态统计",
    textStyle: {
      color: "#fff",
      fontSize: 22.5,
      fontWeight: 500,
    },
    left: "center",
  },
  tooltip: {
    trigger: 'item'
  },
  legend: {
    orient: 'vertical',
    left: 'right',
    textStyle: {
      color: "#fff",
    },
    padding: 25,
  },
  color: ['#ff4d4d', '#043654', '#4b96c4', '#f794ba'],
  series: [
    {
      type: 'pie',
      center: ['50%', '60%'],
      radius: ['45%', '65%'],
      avoidLabelOverlap: false,
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: 40,
          fontWeight: 'bold',
          color: "#fff",
        }
      },
      labelLine: {
        show: false
      },
      data: [
        { value: 1048, name: '小型汽车' },
        { value: 735, name: '中型汽车' },
        { value: 580, name: '大型汽车' },
        { value: 484, name: '学生校车' }
      ]
    }
  ]
});

const option2 = ref({
  title: {
    text: "车辆流入/出曲线图",
    textStyle: {
      color: "#fff",
      fontSize: 22.5,
      fontWeight: 500,
    },
    left: "center",
    top: 5,
  },
  legend: {
    data: ['流入', '流出'],
    textStyle: {
      color: "#fff",
    },
    padding: 40,
  },
  xAxis: {
    type: 'category',
    name: "时间/h",
    data: ['0', '2', '4', '6', '8', '10', '12', '14', '16', '18', '20', '22'],
    axisTick: {
      show: false, // 隐藏刻度线
    },
    axisLabel: {
      color: "#fff",
    },
    axisLine: {
      show: false, // 隐藏坐标轴线
    },
    nameTextStyle: {
      color: "#fff",
    },
  },
  yAxis: {
    type: 'value',
    name: "车流量/百万",
    data: [0, 1, 2, 3, 4, 5, 6],
    axisLabel: {
      color: "#fff",
    },
    nameTextStyle: {
      color: "#fff",
    },
  },
  series: [
    {
      name: '流入',
      type: 'line',
      smooth: true,
      data: [3, 2, 1.5, 2.5, 4, 5, 4, 3.5, 4, 5, 4, 3.5],
      color: "#f81112",
    }, {
      name: '流出',
      type: 'line',
      smooth: true,
      data: [3.5, 1, 2, 2.5, 3, 1, 3, 1, 4, 4.5, 2, 4],
      color: "#5dd3ff",
    },
  ],
  grid: {
    top: '30%',
    right: 60,
    bottom: '10%',
  }
});
</script>
<template>
  <header>
    <HeaderBar />
  </header>
  <div style="height: 83vh; display: flex; justify-content: center;">
    <div class="heat-map">
      <div class="left">
        <div style="height: 35%;"><v-chart :option="option"></v-chart></div>
        <div style="height: 30%;"><v-chart :option="option1"></v-chart></div>
        <div style="height: 35%;"><v-chart :option="option2"></v-chart></div>
      </div>
      <div class="middle" id="center-map">
      </div>
      <div class="right">
        <h2 style="font-weight: 500; margin-top: 5px;">监控视频</h2>
        <div style="width: 100%; display: flex; justify-content: center; height: 40%; margin-bottom: 5%;">
          <video :src="video1" autoplay loop muted style="width: 90%; height: 100%; object-fit: cover;" />
        </div>
        <div style="width: 100%; display: flex; justify-content: center; height: 40%;">
          <video :src="video2" autoplay loop muted style="width: 90%; height: 100%; object-fit: cover;" />
        </div>
        <!-- <div style="height: 25%; margin-bottom: 2%;">
          <video src="/traffic.m4v" autoplay loop muted style="width: 45%; height: 100%; object-fit: cover; margin-right: 2%;" />
          <video src="/traffic2.m4v" autoplay loop muted style="width: 45%; height: 100%; object-fit: cover;" />
        </div>
        <div style="height: 25%;">
          <video src="/traffic.m4v" autoplay loop muted style="width: 45%; height: 100%; object-fit: cover; margin-right: 2%;" />
          <video src="/traffic2.m4v" autoplay loop muted style="width: 45%; height: 100%; object-fit: cover;" />
        </div> -->
      </div>
    </div>
  </div>
</template>
<style scoped>
.heat-map {
  width: 98%;
  height: 100%;
  background: linear-gradient(to bottom, #0e989d, #16263d);
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #fff;
  /* border: 2px solid #000; */
}

.left,
.middle,
.right {
  height: 100%;
}

.left,
.right {
  width: 25%;
  overflow: hidden;
  /* background: #fff; */
}

.middle {
  width: 50%;
  background: #000;
}
</style>