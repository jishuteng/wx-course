<template>
	<!-- 课表 -->
	  <view class="page-box">
	    <view class="header">
	      <view class="currentStatus">今日课表</view>
	      <view class="todayDate">7月13日 | 星期四| 第9周</view>
	    </view>
	    <view class="headerFore"></view>
	    <view class="content ui-BG">
	      <!-- 上午 -->
	      <view class="section">上午课程</view>
	      <view class="class">
	        <view class="time">
	          <view class="start">8:00</view>
	          <view class="end opa">12:00</view>
	        </view>
	        <view class="divider"></view>
	        <view class="infoCan">
	          <view class="infoLesson text-cut">模拟电子技术</view>
	          <view class="infoOther opa">1-4节 | 文教楼203 | 张老师</view>
	        </view>
	      </view>
		  <view class="section">下午课程</view>
		  <view class="class">
		    <view class="time">
		      <view class="start">14:00</view>
		      <view class="end opa">16:00</view>
		    </view>
		    <view class="divider"></view>
		    <view class="infoCan">
		      <view class="infoLesson">计算机网络技术</view>
		      <view class="infoOther opa">4-6节 | 文教楼206 | 文老师</view>
		    </view>
		  </view>
	      
	      <view class="section">晚上课程</view>
	      <view class="class">
	        <view class="time">
	          <view class="start">19:00</view>
	          <view class="end opa">20:30</view>
	        </view>
	        <view class="divider"></view>
	        <view class="infoCan">
	          <view class="infoLesson">大学英语</view>
	          <view class="infoOther opa">8-9节 | 文教楼109 | 吴老师</view>
	        </view>
	      </view>
	      
	    </view>
	  </view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
	.box {
	  margin: 0;
	  padding: 0;
	  border: 0;
	  outline: 0;
	  background: transparent;
	  touch-action: auto;
	  line-height: 1;
	  color: #333;
	}
	
	.wrapper {
	  height: 100vh;
	  position: relative;
	}
	
	.page-box {
	  position: relative;
	  overflow-y: hidden;
	  overflow-x: hidden;
	}
	
	.header {
	  height: 600rpx;
	  background: url(https://cdn.cuuo.cn/images/course-home.png);
	  position: relative;
	  background-size: cover;
	  overflow: auto;
	  z-index: 1;
	}
	
	.todayDate {
	  margin-top: 3vw;
	  margin-left: 8vw;
	  font-weight: 400;
	  font-size: 3.5vw;
	  color: #f1faff;
	  letter-spacing: .9px;
	}
	
	.currentStatus {
	  margin-top: 200rpx;
	  margin-left: 8vw;
	  font-weight: 600;
	  font-size: 5vw;
	  color: #fff;
	}
	
	.tips {
	  position: absolute;
	  background-color: #fff;
	  border-radius: 15rpx;
	  padding: 10rpx;
	  top: 330rpx;
	  right: 18vw;
	  max-width: 500rpx;
	  z-index: 100;
	  opacity: .8;
	  &::after {
	    content: '';
	    position: absolute;
	    height: 20rpx;
	    width: 50rpx;
	    right: -15rpx;
	    top: 25rpx;
	    border-radius: 0rpx 50rpx 0rpx 50rpx;
	    background-color: #fff;
	    z-index: -10;
	    opacity: .8;
	  }
	}
	
	.headerFore {
	  position: absolute;
	  width: 300rpx;
	  height: 235rpx;
	  top: 330rpx;
	  right: -10vw;
	  background: url(https://cdn.cuuo.cn/images/course-tips.gif);
	  background-size: cover;
	  z-index: 100;
	}
	
	.content {
	  position: relative;
	  overflow: auto;
	  margin-top: -100rpx;
	  margin-bottom: 20vw;
	  padding: 2vw 7vw;
	  box-sizing: border-box;
	  background-color: #fff;
	  min-height: calc(100vh -30vw);
	  border-radius: 5vw 5vw 0px 0px;
	  z-index: 10;
	}
	
	.section {
	  margin-top: 6vw;
	  margin-bottom: 3vw;
	  font-size: 3vw;
	  font-weight: 700;
	  letter-spacing: 0;
	  color: #8c93b0;
	}
	
	.class {
	  margin: 20rpx 10rpx;
	  height: 10vw;
	  display: flex;
	  align-items: center;
	}
	
	.opa {
	  opacity: .6;
	}
	
	.noclass {
	  color: #3a526f;
	  opacity: .4;
	}
	
	.time {
	  color: #000;
	  width: 9vw;
	  min-width: 9vw;
	  display: inline-flex;
	  flex-direction: column;
	  margin-right: 1.5vw;
	}
	
	.start {
	  padding-bottom: 10rpx;
	}
	
	.start,
	.end {
	  font-size: 3vw;
	}
	
	.divider {
	  background-color: #2196F3;
	  width: 1vw;
	  min-width: 1vw;
	  height: 8vw;
	  border-radius: 10rpx;
	  color: #0000ff8c;
	}
	
	.infoCan {
	  flex-grow: 1;
	  display: flex;
	  flex-direction: column;
	  margin-left: 2vw;
	  margin-right: 1vw;
	}
	
	.infoLesson,
	.infoOther {
	  color: #000;
	  letter-spacing: 0;
	  margin-bottom: .7vw;
	  white-space: nowrap;
	  overflow: hidden;
	  text-overflow: ellipsis;
	}
	
	.infoLesson {
	  font-size: 4vw;
	  max-width: 590rpx;
	}
	
	.infoOther {
	  font-size: 3vw;
	}
</style>
