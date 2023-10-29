<script setup>
const locations = ['西二环（儿童医院-西直门桥段）', '西三环（丽泽桥-苏州桥段）', '中关村北大街（中关村桥-清华西门段）', '西二环（菜户营桥-广安门桥段）', '长安街（天安门-公主坟段）']
let option = {
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
      textStyle: {
        color: "#fff",
      },
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
        textStyle: {
          color: '#fff',
        },
        formatter: function (params) {
          // params 代表当前数据项
          var value = params.value; // 柱子的数值
          var locationIndex = params.dataIndex; // 获取地点在数组中的索引
          var location = locations[locationIndex] // 获取地点
          return `${location}${value}`
        },
      },
    }
  ]
};
</script>
<template>
  <div style=" height: 83vh; display: flex; justify-content: center;">
    <div class="traffic-info">
      <div class="left">
        <div class="traffic-congestion">
          <v-chart :option="option" style="max-width: 100%;" />
          <div class="traffic-search">
            <h2 style="font-weight: 500;">路段查询</h2>
            <div style="display: flex; flex-direction: row; margin: 0 5%; height: 20%;">
              <span style="display: flex; white-space: nowrap; align-items: center;">
                限行路段：
              </span>
              <el-input v-model="searchInput" placeholder="请输入路段" style="max-width: 50%; margin-right: 20px;" />
              <el-button type="primary" style="border-radius: 10px; height: 100%;">查询</el-button>
            </div>

          </div>
        </div>

      </div>
      <div class="middle"></div>
      <div class="right"></div>
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
</style>

<style>
.el-input__wrapper {
  box-shadow: none !important;
  border: 2px solid #5399c1;
  background-color: #123c54 !important;
  border-radius: 10px !important;
}
</style>