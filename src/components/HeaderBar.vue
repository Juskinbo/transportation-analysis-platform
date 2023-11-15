<script setup>
// import { onMounted } from 'vue';
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';
import ButtonComponent from './ButtonComponent.vue';
import homeBackground from '@/assets/home-header-img.svg';
import SimulationBackground from '@/assets/simulation-header-img.svg';
import heatmapBackground from '@/assets/heatmap-header-img.svg';
const backgroundImage = ref("");
onMounted(() => {
  console.log('HeaderBar mounted!');

  const route = useRoute();


  // 判断路由
  if (route.path === "/") {
    console.log(route.path);
    backgroundImage.value = `url(${homeBackground})`;
  }
  else if (route.path === "/simulation") {
    console.log(route.path);
    backgroundImage.value = `url(${SimulationBackground})`;
  }
  else if (route.path === "/heatmap") {
    console.log(route.path);
    backgroundImage.value = `url(${heatmapBackground})`;
  }
  else {
    console.log(route.path);
    backgroundImage.value = `url(${homeBackground})`;
  }
});


</script>

<template>
  <div class="header-bar">
    <div class="weather">
      <LocationFilled style="height: 30px; color: #3594db; margin-right: 5px;" />
      <span style="font-weight: bold; margin-right: 20px; white-space: nowrap;">杭州市</span>
      <PartlyCloudy style="height: 30px; margin-right: 5px;" />
      <span style="margin-right: 10px; white-space: nowrap;">多云</span>
      <span>25℃~29℃</span>
    </div>
    <div class="title">
      <ButtonComponent position="left-button" text="路段热力图" link="null" style="height: 40%;" />
      <div class="main-title" :style="{ background: backgroundImage }"><span class="main-title-text">智慧交通大数据分析平台</span>
      </div>
      <ButtonComponent position="right-button" text="路段分析" link="null" style="height: 40%;" />
    </div>
    <div class="account-info">
      <el-avatar :size="50" style="margin: 10px;" />
      <span>交通员张三</span>
      <a class="exit">退出</a>
    </div>
  </div>
</template>

<style scoped>
.header-bar {
  display: flex;
  /* 水平居中 */
  justify-content: center;
  align-items: bottom;
  height: 15vh;
  color: #fff;
}

.title {
  width: 60%;
  height: 100%;
  /* background-image: url('/images/header.png'); */
  background-size: 100% 100%;
  background-position: center;
  display: flex;
  align-items: center;
  justify-content: center;

}

.main-title {
  background-size: contain !important;
  background-position: center top !important;
  background-repeat: no-repeat !important;
  height: 100%;
  padding-left: 60px;
  padding-right: 60px;
  display: flex;
  align-items: center;
}

.main-title-text {
  white-space: nowrap;
  font-size: 30px;
  font-weight: 600;
  margin-bottom: 10%;
  /* 文字不显示 */
  color: transparent;
}

.weather,
.account-info {
  /* 垂直居中 */
  display: flex;
  align-items: center;
  width: 20%;
  position: relative;
  margin-right: 1%;
}

.weather {
  /* justify-content: flex-start; */
  margin-left: 1%;
}

.exit {
  position: absolute;
  right: 0;
}
</style>


