<script setup>
import 'echarts/extension/bmap/bmap'
// import data from '@/assets/hangzhou-tracks.json'
import HeaderBar from '../components/HeaderBar.vue'
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
// const route = useRoute()
const router = useRouter()
var map
onMounted(() => {
  var map1 = new BMap.Map("center-map");
  map1.centerAndZoom(new BMap.Point(120.171387, 30.249298), 13);
  var traffic = new BMap.TrafficLayer();        // 创建交通流量图层实例      
  map1.addTileLayer(traffic);
  map1.enableScrollWheelZoom(true);
  map = new BMap.Map("left-map");
  map.centerAndZoom(new BMap.Point(120.171387, 30.249298), 12);
  map.enableScrollWheelZoom(true);
  var traffic1 = new BMap.TrafficLayer();
  map.addTileLayer(traffic1);
})
const warning = ref([
  {
    title: '恶劣天气：泥石流',
    content: '江南大道',
    time: '2023-11-25 16:21:04',
  },
  {
    title: '恶劣天气：强降雨',
    content: '德胜快速路',
    time: '2023-11-25 16:21:04',
  },
  {
    title: '恶劣天气：强降雨',
    content: '九堡大桥',
    time: '2023-11-25 13:25:32',
  },
  {
    title: '重大事件：省人大召开',
    content: '省府路',
    time: '2023-11-25 10:09:19',
  },
  {
    title: '恶劣天气：大风',
    content: '通城高架路',
    time: '2023-11-25 09:25:41',
  },
])
const locations = ['留祥路', '石祥路', '石桥路', '秋涛路', '复兴路']
const option = ref({
  title: {
    text: "路段域拥堵TOP5",
    textStyle: {
      color: "#fff",
      fontSize: 22.5,
      fontWeight: 500,
    },
    left: "center",
    top: 15,
  },
  yAxis: {
    type: 'category',
    data: ['5', '4', '3', '2', '1'],
    axisTick: {
      show: false, // 隐藏刻度线
    },
    axisLine: {
      show: false, // 隐藏坐标轴线
    },
    axisLabel: {
      color: "#fff",
    },
  },
  xAxis: {
    type: 'value',
    show: false
  },
  series: [
    {
      type: 'bar',
      data: [6.0, 6.1, 7.2, 8.7, 9.5],
      barWidth: 15,
      barGap: 0,
      showBackground: true,
      backgroundStyle: {
        color: '#535459'
      },
      itemStyle: {
        color: {
          x: 1,
          y: 1,
          x2: 0,
          y2: 1,
          colorStops: [{
            offset: 0,
            color: '#955151'
          }, {
            offset: 1,
            color: '#222d80'
          }],
          global: false
        },
      },
      label: {
        show: true, // 显示文字
        position: 'top',
        color: '#fff',
        formatter: function (params) {
          // params 代表当前数据项
          var value = params.value; // 柱子的数值
          var locationIndex = params.dataIndex; // 获取地点在数组中的索引
          var location = locations[locationIndex] // 获取地点
          return `${location}\u0020\u0020\u0020\u0020${value}`
        },
      },
    },
  ],
  grid: {
    left: '10%',   // 左边距
    right: '5%',  // 右边距
    bottom: '5%', // 底边距
  },
})
const searchInput = ref("")
const search = () => {
  if (searchInput.value === "") {
    return
  }
  router.push({
    path: '/heatmap',
    query: {
      section: searchInput.value
    }
  })
}

// 定时任务，十秒钟之后添加一个新的数据到 warning 头部
setTimeout(() => {
  warning.value.unshift({
    title: '恶劣天气：大风',
    content: '留石高架路',
    time: '2023-11-25 17:23:41',
  })
  warning.value.pop()
}, 10000)
</script>
<template>
  <header>
    <HeaderBar />
  </header>
  <div style="height: 83vh; display: flex; justify-content: center;">
    <div class="traffic-info">
      <div class="left">
        <div class="traffic-congestion">
          <v-chart :option="option" />
          <div class="section-search">
            <h2 style="font-weight: 500; margin-bottom: 10px;">路段查询</h2>
            <div style="display: flex; flex-direction: row; height: 40px;">
              <span style="display: flex; white-space: nowrap; align-items: center;">
                限行路段：
              </span>
              <el-input v-model="searchInput" placeholder="请输入路段" style="max-width: 50%; margin-right: 20px;" />
              <el-button type="primary" @click="search"
                style="border-radius: 10px; height: 100%; margin-left: auto;">查询</el-button>
            </div>
            <div id="left-map" style="width: 100%; height: 100%; margin-top: 5%;">
            </div>
          </div>
        </div>
      </div>
      <div class="middle" id="center-map">
        <!-- <div>
          <v-chart :option="option3" />
        </div> -->
      </div>
      <div class="right">
        <div class="restricted-section" style="width: 100%; height: 50%;">
          <h2 style="margin: 15px 0 10px; font-weight: 500;">限行路段图</h2>
          <img src="@/assets/restricted-travel-chart.jpg" style="width: 90%; height: 80%;">
        </div>
        <div class="traffic-warning" style="height: 50%; width: 90%;">
          <h2 style="font-weight: 500; margin-bottom: 10px;">交通预报警</h2>
          <ul style="font-size: 12px; line-height: 2.2; white-space: nowrap;">
            <li v-for="o in warning" :key="o.id" style="text-align: left; color: #e74750;">
              <p style="color: white;">{{ o.time }}</p>
              <p style="color: white;">
                <span style="width: 50%;">{{ o.content }}</span>
                <span style="width:50%; float: right;">{{ o.title }}</span>
              </p>
            </li>
          </ul>
          <!-- <v-chart :option="option1" style="width: 100%;" /> -->
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.traffic-info {
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
}

.traffic-congestion {
  height: 50%;
}

.section-search {
  margin: 0 5%;
  height: 100%;
}

.traffic-warning {
  height: 50%;
}

/* ul li::marker {
  font-size: 19px;
} */
</style>

<style>
.el-input__wrapper {
  box-shadow: none !important;
  border: 2px solid #5399c1;
  background-color: #123c54 !important;
  border-radius: 10px !important;
}

/* .ec-extension-bmap {
  width: 49% !important;
  height: 83% !important;
}

.section-search .ec-extension-bmap {
  width: 50% !important;
  height: 50% !important;
} */
</style>