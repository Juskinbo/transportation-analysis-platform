<script setup>
// import { onMounted } from 'vue';
import ButtonComponent from './ButtonComponent.vue';
// import axios from 'axios';
// onMounted(() => {
//   axios({
//     method: "get",
//     url: ""
//   }).then(res => {
//     console.log(res.data);
//   });
// });
</script>

<template>
  <div class="header-bar">
    <div class="weather">
      <LocationFilled style="height: 25%; color: #3594db; margin-right: 5px;" />
      <span style="font-weight: bold; margin-right: 20px;">杭州市</span>
      <PartlyCloudy style="height: 25%; margin-right: 5px;" />
      <span style="margin-right: 10px;">多云</span>
      <span>25℃~29℃</span>
    </div>
    <div class="title">
      <ButtonComponent position="left-button" text="路段热力图" link="null" style="height: 50%;" />
      <div class="main-title"><span class="main-title-text">智慧交通大数据分析平台</span></div>
      <ButtonComponent position="right-button" text="路段分析" link="null" style="height: 50%;" />
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
  height: 80%;
  /* background-image: url('/images/header.png'); */
  background-size: 100% 100%;
  background-position: center;
  display: flex;
  align-items: center;
  justify-content: center;

}

.main-title {
  background: linear-gradient(to bottom, #082037, #2fb2e9);
  height: 100%;
  /* margin-left: 50px; */
  padding-left: 50px;
  padding-right: 50px;
  /* margin-right: 50px; */
  display: flex;
  align-items: center;
}

.main-title-text {
  white-space: nowrap;
  font-size: 30px;
  font-weight: 600;
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
