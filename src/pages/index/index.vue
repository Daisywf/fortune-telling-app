
<template>
  <view class="container">
    <!-- 顶部banner -->
    <view class="banner">
      <image src="https://img.freepik.com/free-vector/magic-crystal-ball-fortune-telling-flat-vector-illustration_74855-17111.jpg" mode="aspectFill"></image>
      <view class="slogan">专为新时代年轻人打造的命理工具</view>
    </view>
    
    <!-- 功能入口区 -->
    <view class="function-area">
      <view class="function-item" @click="navigateTo('/pages/mbti/index')">
        <image src="/static/images/mbti-icon.png"></image>
        <text>MBTI测试</text>
      </view>
      <view class="function-item" @click="navigateTo('/pages/fortune/index')">
        <image src="/static/images/fortune-icon.png"></image>
        <text>命理五行</text>
      </view>
    </view>
    
    <!-- 信息输入区 -->
    <view class="input-area">
      <view class="title">开始你的命理之旅</view>
      <form @submit="handleSubmit">
        <input type="text" v-model="userInfo.name" placeholder="请输入姓名" />
        <picker mode="date" v-model="userInfo.birthday" placeholder="请选择出生日期">
          <view class="picker">{{userInfo.birthday || '请选择出生日期'}}</view>
        </picker>
        <picker mode="selector" :range="genderRange" v-model="userInfo.gender">
          <view class="picker">{{genderRange[userInfo.gender] || '请选择性别'}}</view>
        </picker>
        <button form-type="submit" type="primary">开始分析</button>
      </form>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      userInfo: {
        name: '',
        birthday: '',
        gender: ''
      },
      genderRange: ['男', '女'],
    }
  },
  methods: {
    navigateTo(url) {
      uni.navigateTo({
        url
      })
    },
    handleSubmit() {
      if (!this.userInfo.name || !this.userInfo.birthday || this.userInfo.gender === '') {
        uni.showToast({
          title: '请填写完整信息',
          icon: 'none'
        })
        return
      }
      
      uni.navigateTo({
        url: '/pages/fortune/index',
        success: () => {
          uni.$emit('setUserInfo', this.userInfo)
        }
      })
    }
  }
}
</script>

<style lang="scss">
.container {
  padding: 20rpx;
  
  .banner {
    position: relative;
    height: 300rpx;
    
    image {
      width: 100%;
      height: 100%;
      border-radius: 20rpx;
    }
    
    .slogan {
      position: absolute;
      bottom: 30rpx;
      left: 30rpx;
      color: #fff;
      font-size: 32rpx;
      font-weight: bold;
    }
  }
  
  .function-area {
    display: flex;
    justify-content: space-around;
    margin: 40rpx 0;
    
    .function-item {
      text-align: center;
      
      image {
        width: 120rpx;
        height: 120rpx;
        margin-bottom: 20rpx;
      }
      
      text {
        font-size: 28rpx;
        color: #333;
      }
    }
  }
  
  .input-area {
    background: #fff;
    padding: 30rpx;
    border-radius: 20rpx;
    
    .title {
      font-size: 32rpx;
      font-weight: bold;
      margin-bottom: 30rpx;
    }
    
    input, .picker {
      width: 100%;
      height: 80rpx;
      border: 1rpx solid #eee;
      border-radius: 10rpx;
      margin-bottom: 20rpx;
      padding: 0 20rpx;
      box-sizing: border-box;
    }
    
    button {
      margin-top: 40rpx;
      background: #6B238E;
      
      &::after {
        border: none;
      }
    }
  }
}
</style>
