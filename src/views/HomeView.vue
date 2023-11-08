<script setup>
import 'echarts/extension/bmap/bmap'
import { ref, onMounted } from 'vue'
onMounted(() => {


  var map1 = new BMap.Map("center-map");
  map1.centerAndZoom(new BMap.Point(120.171387, 30.249298), 13);
  var traffic = new BMap.TrafficLayer();        // 创建交通流量图层实例      
  map1.addTileLayer(traffic);                    // 将图层添加到地图上


  var map2 = new BMap.Map("left-map");
  map2.centerAndZoom(new BMap.Point(120.171387, 30.249298), 12);




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
          return `${location}${value}`
        },
      },
    },
  ],
  grid: {
    left: '10%',   // 左边距
    right: '5%',  // 右边距
    bottom: '5%', // 底边距
  },
});

const option1 = ref({
  title: {
    text: "各区市车流量（单位：辆）",
    textStyle: {
      color: "#fff",
      fontSize: 22.5,
      fontWeight: 500,
    },
    left: "center",
    top: 15,
  },
  xAxis: {
    type: 'category',
    data: ['上城区', '下城区', '江干区', '拱墅区', '西湖区', '滨江区', '萧山区', '余杭区', '富阳区', '临安区', '临平区', '钱塘区', '桐庐县', '淳安县', '建德市'],
    axisTick: {
      show: false, // 隐藏刻度线
    },
    axisLine: {
      show: false, // 隐藏坐标轴线
    },
    axisLabel: {
      color: "#fff",
      fontSize: 5,
    },
  },
  yAxis: {
    type: 'value',
    show: false
  },
  series: [
    {
      type: 'pictorialBar',
      data: [26323, 42312, 42342, 44212, 58213, 61223, 57312, 60213, 40924, 32425, 37123, 44821, 38241, 23042, 32453],
      barWidth: 10,
      symbol: 'triangle',
      itemStyle: {
        color: {
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [{
            offset: 0,
            color: '#5cadde'
          }, {
            offset: 1,
            color: '#965253'
          }],
          global: false
        },
        // barBorderRadius: [1, 10, 6, 6]
      },
    },
    {
      type: 'line',
      smooth: true,
      data: [26323, 42312, 42342, 44212, 58213, 61223, 57312, 60213, 40924, 32425, 37123, 44821, 38241, 23042, 32453],
      color: '#866c7a',
      label: {
        show: true, // 显示文字
        position: 'top',
        color: '#fff',
        formatter: '{c}'
      },
    }
  ],
  grid: {
    left: '5%',   // 左边距
    right: '5%',  // 右边距
    bottom: '10%', // 底边距
  }
});
</script>
<template>
  <div style="height: 83vh; display: flex; justify-content: center;">
    <div class="traffic-info">
      <div class="left">
        <div class="traffic-congestion">
          <v-chart :option="option" style="" />
          <div class="section-search">
            <h2 style="font-weight: 500; margin-bottom: 10px;">路段查询</h2>
            <div style="display: flex; flex-direction: row; height: 40px;">
              <span style="display: flex; white-space: nowrap; align-items: center;">
                限行路段：
              </span>
              <el-input v-model="searchInput" placeholder="请输入路段" style="max-width: 50%; margin-right: 20px;" />
              <el-button type="primary" style="border-radius: 10px; height: 100%; margin-left: auto;">查询</el-button>
            </div>
            <div id="left-map" style="width: 100%; height: 100%; margin-top: 5%;">
            </div>
          </div>
        </div>
      </div>
      <div class="middle" id="center-map">
      </div>
      <div class="right">
        <div class="restricted-section" style="width: 100%; height: 50%;">
          <h2 style="margin: 15px 0 10px; font-weight: 500;">限行路段图</h2>
          <img src="@/assets/restricted-travel-chart.jpg" alt="" style="width: 90%; height: 80%;">
        </div>
        <div class="traffic-warning" style="height: 50%; width: 90%;">
          <h2 style="font-weight: 500; margin-bottom: 10px;">交通预报警</h2>
          <ul style="font-size: 12px; line-height: 2.2; white-space: nowrap;">
            <li v-for="o in warning" :key="o.id" style="text-align: left; color: #e74750;">
              <p style="color: white;">{{ o.time }}</p>
              <p style="color: white;">
                <span style="width: 50%;">{{ o.content }}</span>
                <span style="width:50%; float: right;" >{{ o.title }}</span>
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
  background: #000;
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