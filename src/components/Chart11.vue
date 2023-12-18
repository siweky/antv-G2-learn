<template>
  <div>
    <div id="container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Chart } from '@antv/g2';

// 相对定位

const data = ref([
  { genre: 'Sports', sold: 275 },
  { genre: 'Strategy', sold: 115 },
  { genre: 'Action', sold: 120 },
  { genre: 'Shooter', sold: 350 },
  { genre: 'Other', sold: 150 },
])

const renderChart = () => {
  // 初始化图标实例
  const chart = new Chart({
    container: 'container'
  });

  chart
    .interval()
    .coordinate({ type: 'theta', innerRadius: 0.5 })
    .transform({ type: 'stackY' })
    .data(data.value)
    // .encode('x', 'genre')
    .encode('y', 'sold')
    .encode('color', 'genre')

  chart
    .text()
    .style({
      x: 200, // 像素坐标
      y: 200, // 像素坐标
      text: 'hello',
      textAlign: 'center',
      fontSize: 60,
      textBaseline: 'middle',
    })
  chart.on('element.POINTER_ENTER', (a, b, c) => {
    console.log('element:click------', a, b, c)
  });
  chart.render()
}
onMounted(() => {
  renderChart()
})
</script>

<style lang="less" scoped>

</style>