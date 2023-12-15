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
    .line()
    .data({
      type: 'fetch',
      value: 'https://assets.antv.antgroup.com/g2/indices.json',
    })
    .transform({ type: 'normalizeY', basis: 'first', groupBy: 'color' })
    .encode('x', (d) => new Date(d.Date))
    .encode('y', 'Close')
    .encode('color', 'Symbol')
    .axis('y', { title: 'Change in price (%)' })
  chart.render();

}
onMounted(() => {
  renderChart()
})
</script>

<style lang="less" scoped>

</style>