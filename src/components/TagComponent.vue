<script setup>
import { ref } from 'vue'
const props = defineProps({
  value: String
});

const isVisible = ref(true);

const deleteTag = () => {
  // 销毁当前组件
  isVisible.value = false;
}
</script>

<template>
  <div class="tag" v-if="isVisible">
    <div class="value">
      {{ props.value }}
    </div>
    <el-icon @click="deleteTag">
      <Close />
    </el-icon>
  </div>
</template>

<style>
.tag {
  border-radius: 5px;
  background: #3a4450;
  border: 1px solid #00acf5;
  width: fit-content;
  height: fit-content;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 5px 10px;
  margin-right: 20px;
}

.value {
  margin-right: 10px;
}
</style>