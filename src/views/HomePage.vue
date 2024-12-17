<template>
  <div class="page-container">
    <!-- 顶部图片 -->
    <div class="header">
      <img src="@/assets/top.png" alt="header" />
    </div>

    <!-- 主要内容区域 -->
    <div class="home-container">
      <LeftContent />
      <RightContent />
    </div>

    <!-- 底部导航 -->
    <div class="footer">
      <img src="@/assets/menu-btn.png" alt="footer" />
    </div>
  </div>
</template>

<script>
import LeftContent from '@/components/LeftContent.vue'
import RightContent from '@/components/RightContent.vue'

export default {
  name: 'HomePage',
  components: {
    LeftContent,
    RightContent
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
  margin-top: 120px;
}
</style> 