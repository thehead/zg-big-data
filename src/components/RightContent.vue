<template>
  <div class="rightContent">
    <div class="chart-box" :style="{ backgroundImage: `url(${rightBg[0]})` }">
      <div ref="populationChart" class="chart"></div>
      <div class="population-number-container">
        <div class="number-box population-number-one">
          {{ populationNumberOne }}
        </div>
        <div class="number-box population-number-two">
          {{ populationNumberTwo }}
        </div>
        <div class="number-box population-number-three">
          {{ populationNumberThree }}
        </div>
        <div class="number-box population-number-four">
          {{ populationNumberFour }}
        </div>
        <div class="number-box population-number-five">
          {{ populationNumberFive }}
        </div>
      </div>
    </div>
    <div class="chart-box" :style="{ backgroundImage: `url(${rightBg[1]})` }">
      <div ref="constructionChart" class="chart"></div>
    </div>
    <div class="chart-box" :style="{ backgroundImage: `url(${rightBg[2]})` }">
      <div ref="landUseChart" class="chart"></div>
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'RightContent',
  data() {
    return {
      rightBg:[
        require('@/assets/rightBg1.png'),
        require('@/assets/rightBg2.png'),
        require('@/assets/rightBg3.png'),
      ],
      populationNumberOne: '0',
      populationNumberTwo: '0',
      populationNumberThree: '0',
      populationNumberFour: '0',
      populationNumberFive: '0'
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
      
      this.initPopulationChart(commonConfig)
      this.initConstructionChart(commonConfig)
      this.initLandUseChart(commonConfig)
      
      window.addEventListener('resize', () => {
        this.$nextTick(() => {
          const charts = [
            this.$refs.populationChart,
            this.$refs.constructionChart,
            this.$refs.landUseChart
          ].map(ref => echarts.getInstanceByDom(ref))
          
          charts.forEach(chart => {
            chart && chart.resize()
          })
        })
      })
    },
    // 从原文件复制 initPopulationChart, initConstructionChart, initLandUseChart 法
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

      animateValue(17, '', 'populationNumberOne');
      animateValue(10, '', 'populationNumberTwo');
      animateValue(69.93, '%', 'populationNumberThree');
      animateValue(31.07, '%', 'populationNumberFour');
      animateValue(7, '', 'populationNumberFive');
    },
    initPopulationChart(commonConfig) {
      const chart = echarts.init(this.$refs.populationChart, null, commonConfig)
      const option = {
      }
      chart.setOption(option)
    },
    
    initConstructionChart(commonConfig) {
      const chart = echarts.init(this.$refs.constructionChart, null, {
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
        legend: {
          data: ['地上建设面积', '地下建设面积'],
          right: 20,
          top: 62,
          textStyle: {
            color: '#fff',
            fontSize: 14
          },
          itemWidth: 10,
          itemHeight: 10,
          icon: 'circle'
        },
        grid: {
          left: '10%',
          right: '10%',
          top: 100,
          bottom: '10%'
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['xxx区', 'xxx区', 'xxx区', 'xxx区', 'xxx区', 'xxx区'],
          axisLine: {
            show: true,
            lineStyle: {
              color: 'rgba(255, 255, 255, 0.1)'
            }
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#fff',
            fontSize: 14
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: 'rgba(255, 255, 255, 0.1)',
              type: 'dashed'
            }
          }
        },
        yAxis: {
          type: 'value',
          min: 0,
          max: 2000,
          interval: 1000,
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#fff',
            fontSize: 14
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: 'rgba(255, 255, 255, 0.1)',
              type: 'dashed'
            }
          }
        },
        series: [
          {
            name: '地上建设面积',
            type: 'line',
            smooth: true,
            symbol: 'none',
            lineStyle: {
              width: 3,
              color: '#00FFFF'
            },
            areaStyle: {
              opacity: 0.2,
              color: {
                type: 'linear',
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops: [{
                  offset: 0,
                  color: '#00FFFF'
                }, {
                  offset: 1,
                  color: 'rgba(0, 255, 255, 0)'
                }]
              }
            },
            data: [800, 200, 1800, 800, 1000, 500]
          },
          {
            name: '地下建设面积',
            type: 'line',
            smooth: true,
            symbol: 'none',
            lineStyle: {
              width: 3,
              color: '#01CD88'
            },
            areaStyle: {
              opacity: 0.2,
              color: {
                type: 'linear',
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops: [{
                  offset: 0,
                  color: '#01CD88'
                }, {
                  offset: 1,
                  color: 'rgba(1, 205, 136, 0)'
                }]
              }
            },
            data: [500, 1000, 600, 1000, 800, 400]
          }
        ]
      }
      chart.setOption(option)
    },
    
    initLandUseChart(commonConfig) {
      const chart = echarts.init(this.$refs.landUseChart, null, {
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
        legend: {
          data: ['单位：公顷'],
          right: 20,
          top: 62,
          textStyle: {
            color: '#fff',
            fontSize: 14
          }
        },
        grid: {
          left: '10%',
          right: '10%',
          top: 100,
          bottom: '10%',
          containLabel: true
        },
        xAxis: {
          type: 'category',
          data: ['1', '2', '3', '4', '5', '6', '7'],
          axisLine: {
            show: true,
            lineStyle: {
              color: 'rgba(255, 255, 255, 0.1)'
            }
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#fff',
            fontSize: 14
          }
        },
        yAxis: {
          type: 'value',
          min: 0,
          max: 100,
          interval: 20,
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#fff',
            fontSize: 14
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: 'rgba(255, 255, 255, 0.1)',
              type: 'dashed'
            }
          }
        },
        series: [
          {
            type: 'bar',
            data: [18, 28, 28, 48, 28, 88, 28],
            barWidth: 20,
            itemStyle: {
              color: '#09a9f5',
              borderRadius: [4, 4, 0, 0]
            },
            label: {
              show: true,
              position: 'top',
              color: '#fff',
              fontSize: 14,
              formatter: '{c}'
            }
          }
        ]
      }
      chart.setOption(option)
    }
  }
}
</script>

<style lang="scss" scoped>
.rightContent {
  position: fixed;
  top: 90px; 
  bottom: 20px;
  right: 0;
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

  .population-number-one{
    top: 90px;
    left: 80px;
  }
  .population-number-two{
    top: 120px;
    left: 310px;
    font-size: 20px;
  }
  .population-number-three{
    top: 152px;
    left: 376px;
    font-size: 20px;
  }
  .population-number-four{
    top: 186px;
    left: 443px;
    font-size: 20px;
  }
  .population-number-five{
    top: 118px;
    left: 470px;
    font-size: 20px;
  }
}
</style> 