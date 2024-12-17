<template>
  <div class="page-container">
    <!-- 顶部图片 -->
    <div class="header">
      <img src="@/assets/top.png" alt="header" />
    </div>

    <!-- 主要内容区域 -->
    <div class="home-container">
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
    </div>

    <!-- 底部导航 -->
    <div class="footer">
      <img src="@/assets/menu-btn.png" alt="footer" />
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'HomePage',
  mounted() {
    this.initCharts()
    this.startNumberAnimation()
  },
  data(){
    return {
      leftBg:[
        require('@/assets/leftBg1.png'),
        require('@/assets/leftBg2.png'),
        require('@/assets/leftBg3.png'),
      ],
      rightBg:[
        require('@/assets/rightBg1.png'),
        require('@/assets/rightBg2.png'),
        require('@/assets/rightBg3.png'),
      ],
      landNumberOne: '0',
      landNumberTwo: '0',
      resourceNumberOne: '0',
      resourceNumberTwo: '0',
      resourceNumberThree: '0',
      populationNumberOne: '0',
      populationNumberTwo: '0',
      populationNumberThree: '0',
      populationNumberFour: '0',
      populationNumberFive: '0'
    }
  },
  methods: {
    initCharts() {
      // 为所有图表设置统一的背景图片和尺寸
      const commonConfig = {
        width: 559,
        height: 310,
        backgroundColor: {
          image: require('@/assets/chartBg.png')
        }
      }
      
      // 初始化各个图表时传入通用配置
      this.initLandChart(commonConfig)
      this.initCityChart(commonConfig)
      this.initResourceChart(commonConfig)
      this.initPopulationChart(commonConfig)
      this.initConstructionChart(commonConfig)
      this.initLandUseChart(commonConfig)
      
      // 创建一个统一的resize处理函数
      window.addEventListener('resize', () => {
        this.$nextTick(() => {
          // 获取所有图表实例并调用resize
          const charts = [
            this.$refs.landChart,
            this.$refs.cityChart,
            this.$refs.resourceChart,
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
    initLandChart(commonConfig) {
      const chart = echarts.init(this.$refs.landChart, null, commonConfig)
      // 配置图表选项...
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
      
      // 监听窗口大小变化
      window.addEventListener('resize', () => {
        chart.resize()
      })
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
      
      // 监听窗口大小变化
      window.addEventListener('resize', () => {
        chart.resize()
      })
    },
    initResourceChart(commonConfig) {
      const chart = echarts.init(this.$refs.resourceChart, null, commonConfig)
      const option = {
      }
      chart.setOption(option)
      
      window.addEventListener('resize', () => {
        chart.resize()
      })
    },
    initPopulationChart(commonConfig) {
      const chart = echarts.init(this.$refs.populationChart, null, commonConfig)
      const option = {
      }
      chart.setOption(option)
      
      window.addEventListener('resize', () => {
        chart.resize()
      })
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
      
      window.addEventListener('resize', () => {
        chart.resize()
      })
    },
    animateNumber(targetNumber, unit = '') {
      return new Promise((resolve) => {
        let startTime = null;
        const duration = 1000;
        
        const animate = (currentTime) => {
          if (!startTime) startTime = currentTime;
          const elapsed = currentTime - startTime;
          
          // 计算动画进度（0-1之间）
          const progress = Math.min(elapsed / duration, 1);
          
          // 使用 easeOutQuad 缓动函数
          const easeProgress = 1 - Math.pow(1 - progress, 2);
          const currentNumber = targetNumber * easeProgress;
          
          // 根据数字大小决定小数位数
          const decimals = targetNumber >= 100 ? 0 : 1;
          const formattedNumber = currentNumber.toFixed(decimals);
          
          // 返回格式化后的数字加单位
          const result = unit ? `${formattedNumber}${unit}` : formattedNumber;
          
          // 更新当前值
          resolve(result);
          
          if (progress < 1) {
            // 如果动画未完成，继续下一帧
            requestAnimationFrame(animate);
          }
        };

        requestAnimationFrame(animate);
      });
    },
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

      animateValue(17, '', 'populationNumberOne');
      animateValue(10, '', 'populationNumberTwo');
      animateValue(69.93, '%', 'populationNumberThree');
      animateValue(31.07, '%', 'populationNumberFour');
      animateValue(7, '', 'populationNumberFive');
    }
  }
}
</script>

<style lang="scss" scoped>
.page-container {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.header {
  height: 120px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  
  img {
    width: 3014px;
    height: 120px;
    object-fit: contain;
  }
}

.footer {
  height: 110px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  
  img {
    width: 1107px;
    height: 110px;
    object-fit: contain;
  }
}

.home-container {
  position: relative;
  flex: 1;
  width: 100%;
  overflow: hidden;
  margin-top: 120px; // 为顶部留出空间

  .leftContent,
  .rightContent {
    position: fixed;
    top: 90px; 
    bottom: 20px; 
    width: 600px;
    padding: 0 20px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 20px;
    
    /* 隐藏滚动条但保持可滚动 */
    -ms-overflow-style: none;  /* IE and Edge */
    scrollbar-width: none;  /* Firefox */
    &::-webkit-scrollbar {
      display: none;  /* Chrome, Safari and Opera */
    }
  }

  .leftContent {
    left: 0;
  }

  .rightContent {
    right: 0;
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
      top: 226px;
      left: 312px;
      font-size: 40px;
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
      left: 489px;
      font-size: 20px;
    }
  }
}
</style> 