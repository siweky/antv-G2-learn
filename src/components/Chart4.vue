<template>
  <div>
    <div id="container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Chart } from '@antv/g2';

const renderChart = () => {
  // 初始化图标实例
  const chart = new Chart({
    container: 'container'
  });

  chart
    .point()
    .data({
      type: 'fetch',
      value: 'https://gw.alipayobjects.com/os/basement_prod/6b4aa721-b039-49b9-99d8-540b3f87d339.json',
    })
    .encode('x', 'height')
    .encode('y', 'weight')
    // .encode('color', 'gender')
    .encode('color', 'height')
    // .encode('color', 'weight')
  chart.render();

}
onMounted(() => {
  renderChart()
})
</script>

<style lang="less" scoped>

</style>