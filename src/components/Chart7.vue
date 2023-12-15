<template>
  <div>
    <div id="container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Chart } from '@antv/g2';

// 复合Mark  桑基图

const renderChart = () => {
  // 初始化图标实例
  const chart = new Chart({
    container: 'container'
  });

  chart
    .sankey()
    .data({
      type: 'fetch',
      value: 'https://assets.antv.antgroup.com/g2/energy.json',
      transform: [
        {
          type: 'custom',
          callback: (data) => ({ links: data })
        }
      ]
    })
    .layout({
      nodeAlign: 'center',
      nodePadding: 0.03
    })
    // .style({
    //   labelSpacing: 3,
    //   labelFontWeight: 'bold',
    //   nodeStrokeWidth: 1.2,
    //   linkFillOpacity: 0.4
    // })
    .style('labelSpacing', 3)
    .style('labelFontWeight', 'bold')
    .style('nodeStrokeWidth', 1.2)
    .style('linkFillOpacity', 0.4);
  chart.render();

}
onMounted(() => {
  renderChart()
})
</script>

<style lang="less" scoped>

</style>