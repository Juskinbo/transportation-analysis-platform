<script setup>
import 'echarts/extension/bmap/bmap'
import { ref, onMounted } from 'vue'
onMounted(() => {


  var map1 = new BMap.Map("center-map");
  map1.centerAndZoom(new BMap.Point(120.171387, 30.249298), 13);
  var traffic = new BMap.TrafficLayer();        // 创建交通流量图层实例      
  map1.addTileLayer(traffic);                    // 将图层添加到地图上





  // axios({
  //   method: "get",
  //   url: ROOT_PATH + '/data/asset/data/hangzhou-tracks.json'
  // }).then(res => {
  //   console.log(res.data);
  //   points = [].concat.apply(
  //     [],
  //     res.map(function (track) {
  //       return track.map(function (seg) {
  //         return seg.coord.concat([1]);
  //       });
  //     })
  //   )
  // });
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








const warning = [
  {
    id: 1,
    title: '恶劣天气：泥石流',
    content: '北侧交通路口',
    time: '2023-10-12 16:25:32',
  },
  {
    id: 2,
    title: '重大事件：省人大召开',
    content: '北侧交通路口',
    time: '2023-10-12 16:25:32',
  },
  {
    id: 3,
    title: '恶劣天气：泥石流',
    content: '北侧交通路口',
    time: '2023-10-12 16:25:32',
  },
  {
    id: 4,
    title: '重大事件：省人大召开',
    content: '北侧交通路口',
    time: '2023-10-12 16:25:32',
  },
  {
    id: 5,
    title: '恶劣天气：泥石流',
    content: '北侧交通路口',
    time: '2023-10-12 16:25:32',
  },
]


const locations = ['西二环（儿童医院-西直门桥段）', '西三环（丽泽桥-苏州桥段）', '中关村北大街（中关村桥-清华西门段）', '西二环（菜户营桥-广安门桥段）', '长安街（天安门-公主坟段）']


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
  },
  series: [
    {
      type: 'pie',
      center: ['50%', '55%'],
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
          fontWeight: 'bold'
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


</script>
<template>
  <div style="height: 83vh; display: flex; justify-content: center;">
    <div class="heat-map">
      <div class="left">
        <div style="height: 35%;"><v-chart :option="option"></v-chart></div>
        <div style="height: 30%;"><v-chart :option="option1"></v-chart></div>
        <div style="height: 35%;"><v-chart :option="option"></v-chart></div>
      </div>
      <div class="middle" id="center-map">
      </div>
      <div class="right">

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