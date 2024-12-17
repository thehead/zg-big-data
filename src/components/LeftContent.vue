<template>
  <div class="leftContent">
    <div class="chart-box" :style="{ backgroundImage: `url(${leftBg[0]})` }">
      <div ref="landChart" class="chart"></div>
      <div class="land-number-container">
        <div class="number-box land-number-one">
          {{ landNumberOne }}
        </div>
        <div class="number-box land-number-two">
          {{ landNumberTwo }}
        </div>
      </div>
    </div>
    <div class="chart-box" :style="{ backgroundImage: `url(${leftBg[1]})` }">
      <div ref="cityChart" class="chart"></div>
    </div>
    <div class="chart-box" :style="{ backgroundImage: `url(${leftBg[2]})` }">
      <div ref="resourceChart" class="chart"></div>
      <div class="resource-number-container">
        <div class="number-box resource-number-one">
          {{ resourceNumberOne }}
        </div>
        <div class="number-box resource-number-two">
          {{ resourceNumberTwo }}
        </div>
        <div class="number-box resource-number-three">
          {{ resourceNumberThree }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'LeftContent',
  data() {
    return {
      leftBg:[
        require('@/assets/leftBg1.png'),
        require('@/assets/leftBg2.png'),
        require('@/assets/leftBg3.png'),
      ],
      landNumberOne: '0',
      landNumberTwo: '0',
      resourceNumberOne: '0',
      resourceNumberTwo: '0',
      resourceNumberThree: '0',
    }
  },
  mounted() {
    this.initCharts()
    this.startNumberAnimation()
  },
  methods: {
    initCharts() {
      const commonConfig = {
        width: 559,
        height: 310,
        backgroundColor: {
          image: require('@/assets/chartBg.png')
        }
      }
      
      this.initLandChart(commonConfig)
      this.initCityChart(commonConfig)
      this.initResourceChart(commonConfig)
      
      window.addEventListener('resize', () => {
        this.$nextTick(() => {
          const charts = [
            this.$refs.landChart,
            this.$refs.cityChart,
            this.$refs.resourceChart
          ].map(ref => echarts.getInstanceByDom(ref))
          
          charts.forEach(chart => {
            chart && chart.resize()
          })
        })
      })
    },
    // 从原文件复制 initLandChart, initCityChart, initResourceChart 方法
    async startNumberAnimation() {
      const animateValue = async (target, unit, prop) => {
        let startTime = null;
        const duration = 1300;

        const updateFrame = (currentTime) => {
          if (!startTime) startTime = currentTime;
          const elapsed = currentTime - startTime;
          const progress = Math.min(elapsed / duration, 1);
          
          const easeProgress = 1 - Math.pow(1 - progress, 2);
          const currentNumber = target * easeProgress;
          
          const decimals = target >= 100 ? 0 : 1;
          const formattedNumber = currentNumber.toFixed(decimals);
          
          this[prop] = unit ? `${formattedNumber}${unit}` : formattedNumber;
          
          if (progress < 1) {
            requestAnimationFrame(updateFrame);
          }
        };

        requestAnimationFrame(updateFrame);
      };

      animateValue(530, '', 'landNumberOne');
      animateValue(54, '%', 'landNumberTwo');
      animateValue(70, '%', 'resourceNumberOne');
      animateValue(30, '%', 'resourceNumberTwo');
      animateValue(24542, '', 'resourceNumberThree');
    },
    initLandChart(commonConfig) {
      const chart = echarts.init(this.$refs.landChart, null, commonConfig)
      const option = {
      }
      chart.setOption(option)
    },
    
    initCityChart(commonConfig) {
      const chart = echarts.init(this.$refs.cityChart, null, {
        ...commonConfig,
        width: 559,
        height: 295
      })
      const option = {
        title: {
          textStyle: {
            color: '#fff',
            fontSize: 16,
            fontWeight: 'normal'
          },
          left: 20,
          top: 0
        },
        grid: {
          left: '15%',
          right: '15%',
          top: 62,
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            show: false
          },
          splitLine: {
            show: false
          }
        },
        yAxis: {
          type: 'category',
          data: ['绿化广场', '工业存储', '公共设施', '农村居住', '城镇居'],
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#fff',
            fontSize: 16,
            margin: 20
          }
        },
        series: [
          {
            type: 'bar',
            data: [368, 408, 484, 521, 604],
            barWidth: 8,
            itemStyle: {
              color: {
                type: 'linear',
                x: 0,
                y: 0,
                x2: 1,
                y2: 0,
                colorStops: [{
                  offset: 0,
                  color: '#09a9f5'
                }, {
                  offset: 1,
                  color: '#09a9f5'
                }]
              },
              borderRadius: [0, 4, 4, 0]
            },
            label: {
              show: true,
              position: 'right',
              color: '#fff',
              fontSize: 16,
              distance: 15,
              formatter: '{c}'
            }
          },
          {
            type: 'bar',
            data: [368, 408, 484, 521, 604],
            barWidth: 8,
            barGap: '-100%',
            itemStyle: {
              color: 'rgba(9, 169, 245, 0.1)'
            },
            label: {
              show: false
            }
          }
        ]
      }
      chart.setOption(option)
    },
    
    initResourceChart(commonConfig) {
      const chart = echarts.init(this.$refs.resourceChart, null, commonConfig)
      const option = {
      }
      chart.setOption(option)
    }
  }
}
</script>

<style lang="scss" scoped>
.leftContent {
  position: fixed;
  top: 90px; 
  bottom: 20px;
  left: 0;
  width: 600px;
  padding: 0 20px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
  
  -ms-overflow-style: none;
  scrollbar-width: none;
  &::-webkit-scrollbar {
    display: none;
  }
}

.chart-box {
  position: relative;
  flex: 0 0 auto;
  width: 559px;
  height: 310px;
  margin: 0 auto;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;

  .chart {
    height: 100% !important;
    width: 100% !important;
    margin: 0 auto;
  }

  .number-box{
    position: absolute;
    z-index: 10;
    color: #fff;
    font-size: 30px;
    font-weight: bold;
  }
  .land-number-one{
    top: 131px;
    left: 383px;
    font-size: 32px;
  }
  .land-number-two{
    top: 229px;
    left: 383px;
    font-size: 32px; 
  }
  .resource-number-one{
    top: 146px;
    left: 160px;
  }
  .resource-number-two{
    top: 146px;
    left: 408px;
  }
  .resource-number-three{
    top: 236px;
    left: 312px;
    font-size: 40px;
  }
}
</style> 