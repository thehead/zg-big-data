<template>
  <div class="app-container">
    <div class="background" :style="backgroundStyle">
      <header class="header">
        <h1 class="title">自贡城市信息模型平台</h1>
        <div class="nav-top">
          <span>城市运行</span>
          <span>经济运行</span>
          <span>交通运行</span>
        </div>
        <div class="header-right">
          <span class="weather">28°</span>
          <span class="battery">20%</span>
        </div>
      </header>
      
      <router-view></router-view>

      <footer class="footer-nav">
        <div class="nav-item">土地规划</div>
        <div class="nav-item">规划范围</div>
        <div class="nav-item">产业用地</div>
        <div class="nav-item">总体规划</div>
        <div class="nav-item">专题查控</div>
      </footer>
    </div>
  </div>
</template>

<script>
import bgImage from '@/assets/bg.jpg'

export default {
  name: 'App',
  data() {
    return {
      bgImage
    }
  },
  computed: {
    backgroundStyle() {
      return {
        background: `url(${this.bgImage}) no-repeat center center`,
        backgroundSize: 'cover'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.app-container {
  width: 3840px;
  height: 1080px;
  overflow: hidden;
  
  .background {
    width: 100%;
    height: 100%;
    position: relative;
  }

  .header {
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 40px;
    background: rgba(0,0,0,0.3);

    .title {
      color: #fff;
      font-size: 32px;
    }

    .nav-top {
      span {
        color: #fff;
        margin: 0 20px;
        cursor: pointer;
        
        &:hover {
          color: #409EFF;
        }
      }
    }

    .header-right {
      color: #fff;
      
      span {
        margin-left: 20px;
      }
    }
  }

  .footer-nav {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(0,0,0,0.3);

    .nav-item {
      color: #fff;
      margin: 0 30px;
      cursor: pointer;
      
      &:hover {
        color: #409EFF;
      }
    }
  }
}
</style> 