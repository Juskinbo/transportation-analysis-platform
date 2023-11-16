<script setup>
import 'echarts/extension/bmap/bmap'
import HeaderBar from '../components/HeaderBar.vue';
import { ref, onMounted } from 'vue'
import {useRoute } from 'vue-router'
const route = useRoute()
onMounted(() => {


  var map1 = new BMap.Map("center-map");
  map1.centerAndZoom(new BMap.Point(120.171387, 30.249298), 13);
  var traffic = new BMap.TrafficLayer();        // 创建交通流量图层实例      
  map1.addTileLayer(traffic);                    // 将图层添加到地图上

  map1.enableScrollWheelZoom(true); 

})
// let option1 = {
//   animation: false,
//   bmap: {
//     center: [120.13066322374, 30.240018034923],
//     zoom: 14,
//     roam: true,
//     trafficLayer: true,
//   },
//   visualMap: {
//     show: false,
//     top: 'top',
//     min: 0,
//     max: 5,
//     seriesIndex: 0,
//     calculable: true,
//     inRange: {
//       color: ['blue', 'blue', 'green', 'yellow', 'red']
//     }
//   },
//   series: [
//     {
//       type: 'heatmap',
//       coordinateSystem: 'bmap',
//       data: points,
//       pointSize: 5,
//       blurSize: 6
//     }
//   ]
// }

// // 添加百度地图插件
// var bmap = myChart.getModel().getComponent('bmap').getBMap();
// bmap.addControl(new BMap.MapTypeControl());

const option = ref({
  title: {
    text: "路段车流量预计变化趋势",
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
      data: [3, 2, 1.5, 2.5, 4, 5, 4, 3.5, 4, 5, 4, 3.5],
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
    text: "路段车流量预计变化趋势",
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
      data: [3, 2, 1.5, 2.5, 4, 5, 4, 3.5, 4, 5, 4, 3.5],
      color: "#f81112",
    }, {
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
          <video src="/traffic.m4v" autoplay loop muted style="width: 90%; height: 100%; object-fit: cover;" />
        </div>
        <div style="width: 100%; display: flex; justify-content: center; height: 40%;">
          <video src="/traffic2.m4v" autoplay loop muted style="width: 90%; height: 100%; object-fit: cover;" />
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