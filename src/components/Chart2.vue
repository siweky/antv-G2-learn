<template>
  <div>
    <div id="container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Chart } from '@antv/g2';

const data = ref([
  { year: '1991', value: 3 },
  { year: '1992', value: 4 },
  { year: '1993', value: 3.5 },
  { year: '1994', value: 5 },
  { year: '1995', value: 4.9 },
  { year: '1996', value: 6 },
  { year: '1997', value: 7 },
  { year: '1998', value: 9 },
  { year: '1999', value: 13 },
]);

const renderChart = () => {
  // 初始化图标实例
  const chart = new Chart({
    container: 'container'
  });

  // 声明可视化
  chart
    .line()
    .data(data.value) // 绑定数据
    .encode('x', 'year') // 编码x通道
    .encode('y', 'value') // 编码y通道
  chart
    .point() // 创建一个 Interval 标记
    .data(data.value) // 绑定数据
    .encode('x', 'year') // 编码x通道
    .encode('y', 'value') // 编码y通道
    // 渲染可视化
  chart.render();

}
onMounted(() => {
  renderChart()
})
</script>

<style lang="less" scoped>

</style>