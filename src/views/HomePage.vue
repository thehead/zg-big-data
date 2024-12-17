<template>
  <div class="home-container">
    <div class="left-panel">
      <div class="chart-box">
        <h3>建设用地规划</h3>
        <div ref="landChart" class="chart"></div>
      </div>
      <div class="chart-box">
        <h3>城市用地规划</h3>
        <div ref="cityChart" class="chart"></div>
      </div>
      <div class="chart-box">
        <h3>基础资源用量</h3>
        <div ref="resourceChart" class="chart"></div>
      </div>
    </div>
    
    <div class="center-content">
      <!-- 中间3D地图内容 -->
    </div>
    
    <div class="right-panel">
      <div class="chart-box">
        <h3>人口统计</h3>
        <div ref="populationChart" class="chart"></div>
      </div>
      <div class="chart-box">
        <h3>建设规模</h3>
        <div ref="constructionChart" class="chart"></div>
      </div>
      <div class="chart-box">
        <h3>土地规划用地</h3>
        <div ref="landUseChart" class="chart"></div>
      </div>
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'HomePage',
  mounted() {
    this.initCharts()
  },
  methods: {
    initCharts() {
      // 初始化各个图表
      this.initLandChart()
      this.initCityChart()
      this.initResourceChart()
      this.initPopulationChart()
      this.initConstructionChart()
      this.initLandUseChart()
    },
    initLandChart() {
      const chart = echarts.init(this.$refs.landChart)
      // 配置图表选项...
    },
    initCityChart() {
      const chart = echarts.init(this.$refs.cityChart)
      const option = {
        title: {
          text: '单位: 平方公里',
          textStyle: {
            color: '#fff',
            fontSize: 16,
            fontWeight: 'normal'
          },
          left: 20,
          top: 0
        },
        grid: {
          left: '20%',
          right: '20%',
          top: '10%',
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
                  color: '#00FFFF'
                }, {
                  offset: 1,
                  color: '#00FFFF'
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
              color: 'rgba(0, 255, 255, 0.1)'
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
    initConstructionChart() {
      const chart = echarts.init(this.$refs.constructionChart)
      const option = {
        title: {
          text: '单位: 万平方米',
          textStyle: {
            color: '#fff',
            fontSize: 16,
            fontWeight: 'normal'
          },
          left: 20,
          top: 0
        },
        grid: {
          left: '10%',
          right: '10%',
          top: '15%',
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
        ],
        legend: {
          data: ['地上建设面积', '地下建设面积'],
          right: 20,
          top: 0,
          textStyle: {
            color: '#fff',
            fontSize: 14
          },
          itemWidth: 10,
          itemHeight: 10,
          icon: 'circle'
        }
      }
      
      chart.setOption(option)
      
      // 监听窗口大小变化
      window.addEventListener('resize', () => {
        chart.resize()
      })
    },
    initResourceChart() {
      const chart = echarts.init(this.$refs.resourceChart)
      const option = {
        // 基础资源用量的配置将在后续添加
      }
      chart.setOption(option)
      
      window.addEventListener('resize', () => {
        chart.resize()
      })
    },
    initPopulationChart() {
      const chart = echarts.init(this.$refs.populationChart)
      const option = {
        // 人口统计的配置将在后续添加
      }
      chart.setOption(option)
      
      window.addEventListener('resize', () => {
        chart.resize()
      })
    },
    initLandUseChart() {
      const chart = echarts.init(this.$refs.landUseChart)
      const option = {
        // 土地规划用地的配置将在后续添加
      }
      chart.setOption(option)
      
      window.addEventListener('resize', () => {
        chart.resize()
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.home-container {
  display: flex;
  height: calc(100vh - 120px);
  padding: 20px 0;
  justify-content: space-between;

  .left-panel,
  .right-panel {
    width: 35%;
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 0 20px;
  }

  .center-content {
    width: 30%;
    padding: 0 10px;
  }

  .chart-box {
    flex: 1;
    background: rgba(0,24,106,0.6);
    border: 1px solid rgba(0,170,255,0.3);
    padding: 15px;
    border-radius: 4px;

    h3 {
      color: #fff;
      margin: 0 0 15px 0;
      font-size: 18px;
    }

    .chart {
      height: calc(100% - 30px);
      width: 100%;
    }
  }
}
</style> 