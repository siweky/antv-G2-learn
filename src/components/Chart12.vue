<template>
  <div>
    <div id="container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue';
import { Chart, ChartEvent } from '@antv/g2';

// 词云图
const _data = ref([])

const renderChart = () => {
  // 初始化图标实例
  const chart = new Chart({
    container: 'container'
  });

  chart
    .wordCloud()
    // .data({
    //   type: 'fetch',
    //   // value: _data.value
    //   value: 'https://assets.antv.antgroup.com/g2/philosophy-word.json',
    // })
    .data(_data.value)
    .layout({
      spiral: 'rectangular',
      padding: 3,
      random: 1,
      rotate: ((v, index) => {
        return 45 * (index % 4)
      }),
    })
    .encode('color', 'text')
    .axis(false)
    .legend(false)
    // .tooltip({
    //   title: 'text',
    //   items: [{ channel: 'value' }],
    // })
    // .tooltip({
    //   show: true, // 是否显示工具提示
    //   formatter: (d) => `${d.name}: ${d.value}`, // 自定义工具提示的内容格式
    // })
    .tooltip({
      title: (d) => new Date(d.Date).toUTCString(),
      items: [
        (d, i, data, column) => ({
          name: 'text',
          value: 11,
        }),
      ],
    })

  const tooltipContainer = document.createElement('div');
  tooltipContainer.classList.add('g2-tooltip');
  document.body.appendChild(tooltipContainer);
  // 鼠标移入显示tooltip
  chart.on(`element:${ChartEvent.POINTER_MOVE}`, (ev) => {
    // console.log('%c POINTER_MOVE', 'background: red', ev);
    const { x, y } = ev.global;
    const { text, value } = ev.data.data;
    const { fill } = ev.target.attributes;
    tooltipContainer.innerHTML = `
      <div class="g2-tooltip-item">
        <span class="g2-tooltip-marker" style="background-color: ${fill}"></span>
        <span class="g2-tooltip-name">${text}</span>
        <span class="g2-tooltip-value">${value}</span>
      </div>`;
    tooltipContainer.style.display = 'block';
    tooltipContainer.style.left = `${x + 12}px`;
    tooltipContainer.style.top = `${y + 12}px`;
  });
  // 鼠标移除隐藏tooltip
  chart.on(`element:${ChartEvent.POINTER_OUT}`, (ev) => {
    // console.log('%c POINTER_OUT', 'background: red', ev);
    // clearTooltip();
    tooltipContainer.style.display = 'none';
  });
  chart.render();
}
onMounted(() => {
  for (let i = 0; i < 100; i++) {
    _data.value.push({
      value: Math.ceil(Math.random() * 100),
      text: `标签${i}`,
      name: `萨特${i}`
    })
  }
  nextTick(() => {
    renderChart()
  })
})
</script>

<style>
.g2-tooltip {
  display: none;
  position: absolute;
  background-color: rgba(255, 255, 255, 0.96);
  box-shadow: rgba(0, 0, 0, 0.12) 0px 6px 12px 0px;
  border-radius: 4px;
  padding: 12px;
  font-size: 12px;
  line-height: 2;
}

.g2-tooltip-item {
  display: flex;
  align-items: center;
  gap: 4px;
}

.g2-tooltip-item span {
  display: block;
}

.g2-tooltip-marker {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.g2-tooltip-name {
  color: rgba(0, 0, 0, 0.65);
}

.g2-tooltip-value {
  margin-left: 30px;
  color: rgba(0, 0, 0, 0.85);
}</style>