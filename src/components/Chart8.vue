<template>
  <div>
    <div id="container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Chart } from '@antv/g2';

// 转换

const renderChart = () => {
  // 初始化图标实例
  const chart = new Chart({
    container: 'container'
  });

  chart.data({
    type: 'fetch',
    value: 'https://gw.alipayobjects.com/os/bmw-prod/1ecf85d2-8279-46a1-898d-d2e1814617f9.json',
  })

  chart
    .point()
    .encode('x', 'GDP')
    .encode('y', 'LifeExpectancy')
    .encode('color', 'Continent');

  chart
    .text()
    // 将图形按照 series 分组，也就是 Continent
    // 通过 x 通道选择，选择其中最大的，也就是 GDP 最大的
    .transform({ type: 'select', channel: 'x', selector: 'max' })
    .encode('text', 'Country')
    .encode('x', 'GDP')
    .encode('y', 'LifeExpectancy')
    .encode('series', 'Continent')
    .style('textAlign', 'end');

  chart.render()
}
onMounted(() => {
  renderChart()
})
</script>

<style lang="less" scoped>

</style>