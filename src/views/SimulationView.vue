<script setup>
import { onMounted, ref } from 'vue';
onMounted(() => {
  var map = new BMap.Map("simulation-map");
  map.centerAndZoom(new BMap.Point(120.171387, 30.249298), 13);
  var traffic = new BMap.TrafficLayer();        // 创建交通流量图层实例      
  map.addTileLayer(traffic);                    // 将图层添加到地图上
});

const option = ref({
  title: {
    text: "路段车流量预计变化趋势",
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

const simulationItems = ref([
  {
    index: 1,
    time: "2023-10-12 16:25:32",
    type: "和平南路 单号 蓝牌小轿车"
  },
  {
    index: 2,
    time: "2023-10-12 16:25:32",
    type: "和平南路 单号 蓝牌小轿车"
  },
  {
    index: 3,
    time: "2023-10-12 16:25:32",
    type: "和平南路 单号 蓝牌小轿车"
  },
  {
    index: 4,
    time: "2023-10-12 16:25:32",
    type: "和平南路 单号 蓝牌小轿车"
  }
])

const schemeTitles = ref(["", "限行时段", "限行规则", "限行范围"])
</script>
<template>
  <div style="height: 83vh; display: flex; justify-content: center;">
    <div class="simulation-info">
      <div class=left>
        <div class="simulation-selection">
          <div class="simulation-form">
            <div class="simulation-input">
              <div class="tag-input">
                <h3 style="width: 50%; text-align: left;">
                  输入标签：
                </h3>
                <el-input style="width: 50%;" placeholder="请输入标签"> </el-input>
              </div>
              <div class="section-input">
                <h3 style="width: 50%; text-align: left;">
                  输入模拟路段：
                </h3>
                <el-select style="width: 50%;" placeholder="请输入模拟路段名"></el-select>
              </div>
            </div>
            <div class="simulation-tag">
              <!-- 展示所有标签 -->
            </div>
          </div>
          <div class="simulation-button">
            <el-button type="info">重置</el-button>
            <el-button type="primary">模拟</el-button>
          </div>
        </div>
        <div class="simulation-data">
          <div class="simulation-chart">
            <div class="changing-trends">
              <v-chart :option="option"></v-chart>
            </div>
            <div class="pressure-analysis">
              <v-chart :option="option"></v-chart>
            </div>
          </div>
          <div class="section-simulation">
            <h2 style="font-weight: 500; margin: 15px 0 10px; line-height: normal;">路段模拟热力图</h2>
            <div id="simulation-map" style="flex: 1; width: 100%;"></div>
          </div>
        </div>
      </div>
      <div class="right">
        <div class="simulation-history">
          <div style="width: 100%; background: linear-gradient(to bottom, #fc333d, #762528)">模拟记录</div>
          <div class="simulation-count">
            <span style="font-size: 38px; font-weight: 600; color:  #e74750;">24</span>
          </div>
          <div class="simulation-item">
            <div style="">
              <ul style="line-height: 1.3;">
                <li v-for="o in simulationItems" :key="o.index" style="margin-top: 10px;">
                  <p>{{ o.time }}</p>
                  <p>{{ o.type }}</p>
                </li>
              </ul>
            </div>
            <div class="scheme-generation">
              <el-button text style="width: 40%; color: white; background: linear-gradient(to bottom, #fd333e, #762429);">
                方案生成
              </el-button>
            </div>
          </div>
        </div>
        <div class="restriction-scheme">
          <div style="background: linear-gradient(to bottom, #fc333d, #762528); width: 100%;">限行方案</div>
          <div style="display: grid; font-size: 12px; width: 90%;">
            <div style="display: grid; grid-template-columns: repeat(4, 1fr); margin: 10px 0;">
              <div v-for="o, index in schemeTitles" :key="index">{{ o }}</div>
            </div>
            <div style="display: grid; grid-template-columns: repeat(4, 1fr);">
              <div style="margin: 5px 5px; display: flex; align-items: center;">浙A号牌</div>
              <div style="grid-column: span 3; background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">
                不变，限行时段、范围和规则都维持不变</div>
              <div style="grid-row: span 2; margin: 5px 5px; display: flex; align-items: center;">非浙A号牌</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">7:00-9:00<br>16:30-18:30</div>
              <div
                style="grid-row: span 2; background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px; display: flex; align-items: center; justify-content: center;">
                全号段限行</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">绕城高速公路范围内的所有道路</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">7:00-9:00<br>16:30-18:30</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">绕城高速公路范围内的所有道路</div>
              <div style="grid-row: span 3; margin: 5px 5px; display: flex; align-items: center;">浙A区域号牌</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">7:00-9:00<br>16:30-18:30</div>
              <div
                style="grid-row: span 2; background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px; display: flex; align-items: center; justify-content: center;">
                全号段限行</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">绕城高速公路范围内的所有道路</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">7:00-9:00<br>16:30-18:30</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">绕城高速公路范围内的所有道路</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">7:00-9:00<br>16:30-18:30</div>
              <div
                style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px; display: flex; align-items: center; justify-content: center;">
                尾号限行</div>
              <div style="background-color: #2eb3e9; border-radius: 4px; margin: 5px 5px;">绕城高速公路范围内的所有道路</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.simulation-info {
  width: 98%;
  height: 100%;
  background: linear-gradient(to bottom, #0e989d, #16263d);
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #fff;
}

.left {
  width: 70%;
  height: 100%;
}

.right {
  width: 30%;
  height: 100%;
  background-color: #0d4b68;
}

.simulation-selection {
  width: 100%;
  height: 25%;
  /* background-color: red; */
  display: flex;
  align-items: center;
}

.simulation-form {
  width: 90%;
  height: 90%;
  margin-left: 15px;
  border: 2px solid #049dc3;
  border-radius: 5px;
  background-color: #0e989d;
  display: inline-flex;
}

.simulation-input {
  background-color: #377b7e;
  width: 35%;
  height: 100%;
  border-right: 2px solid #049dc3;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 0 1%;
}


.simulation-tag {
  background-color: #0e586d;
  width: 65%;
  height: 100%;
}

.simulation-button {
  display: flex;
  width: 10%;
  padding: 0 15px;
  flex-direction: column;
}

.tag-input {
  display: flex;
  white-space: nowrap;
  margin: 5% 0;
  align-items: center;
}

.section-input {
  display: flex;
  white-space: nowrap;
  margin: 5% 0;
  align-items: center;
}

.simulation-data {
  height: 75%;
  display: flex;
}

.simulation-chart {
  width: 40%;
  height: 100%;
}

.changing-trends {
  height: 50%;
}

.pressure-analysis {
  height: 50%;
}

.section-simulation {
  width: 60%;
  height: 100%;
  display: flex;
  flex-direction: column;
  margin-right: 15px;
}

.simulation-history {
  height: 50%;
  display: flex;
  flex-direction: column;
  /* display: flex; */
  align-items: center;
}

.restriction-scheme {
  max-height: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.simulation-count {
  background-color: #84acba;
  width: 100%;
  height: 20%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 3px solid #e74750;
}

.simulation-item {
  display: flex;
  width: 80%;
  font-size: 12px;
  margin: 0 5%;
  text-align: left;
  flex-direction: column;
  flex: 1;
  overflow: hidden;
}

.simulation-item li::marker {
  color: #e74750;
}

.scheme-generation {
  display: flex;
  justify-content: center;
  margin-top: auto;
  align-items: center;
  flex: 1;
}






.el-button+.el-button {
  margin-left: 0;
  margin: 10px 0;
}</style>

<style></style>