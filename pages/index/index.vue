<template>
	<view class="content">
		<view class="uni-margin-wrap">
			<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
				<swiper-item>
					<image src="/static/swiper/jyzd.png" class="lunbo"></image>
				</swiper-item>
				<swiper-item>
					<image src="/static/swiper/zxfw.png" class="lunbo"></image>
				</swiper-item>
				<swiper-item>
					<image src="/static/swiper/xqjh.png" class="lunbo"></image>
				</swiper-item>
			</swiper>
		</view>
		<view class="warp">
			<uni-section title="功能模块" padding="20" type="line">
				<view style="display: flex;margin-top:5rpx ;">
					<view style="background-color: lightgray; width: 100%; height: 1rpx;"></view>
				</view>
				<uni-grid :column="4" :highlight="true" @change="change" :show-border="false">
					<uni-grid-item v-for="(item, index) in list" :index="index" :key="index">
						<view class="grid-item-box" style="background-color: #FFF;" v-if="index == 1" @click="cxcj">
							<image :src=item.url style="width: 40px;height:40px;"></image>
							<text class="text">{{item.text}}</text>
						</view>
						<view class="grid-item-box" style="background-color: #FFF;" v-else>
							<image :src=item.url style="width: 40px;height:40px;"></image>
							<text class="text">{{item.text}}</text>
						</view>
					</uni-grid-item>
				</uni-grid>
			</uni-section>
		</view>
		<uni-section title="信息资讯" type="line">
			<view v-for="(value, key) in listData" :key="key" @click="goDetail(value)" class="info">
				<uni-list-chat :title="value.title" :avatar="value.avatar" :note="value.note">
				</uni-list-chat>
				<view class="infoContent"></view>
				<uni-row :width="nvueWidth">
					<uni-col :span="10">
						<view class="interaction" style="margin-left: 30upx;">日期:{{value.pub_at}}</view>
					</uni-col>
					<uni-col :span="14">
						<view class="interaction">{{value.source}}</view>
					</uni-col>
				</uni-row>
			</view>
		</uni-section>
		<uv-divider text="已经到底了"></uv-divider>
	</view>
</template>

<script>
	export default {
		components: {},
		data() {
			return {
				url: 'http://xk.huel.edu.cn/jwglxt/xtgl/login_slogin.html',
				nvueWidth: 730,
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				list: [{
						url: '/static/function/kbcx.png',
						text: '课表查询',
						badge: '0',
						type: "primary"
					},
					{
						url: '/static/function/cjcx.png',
						text: '成绩查询',
						badge: '1',
						type: "success"
					},
					{
						url: '/static/function/remind.png',
						text: '课程通知',
						badge: '2',
						type: "error"
					}, {
						url: '/static/function/guide.png',
						text: '信息资讯',
						badge: '3',
						type: "warning"
					}
				],
				//信息资讯列表数据
				listData: [{
						id: "1",
						title: "梳理新问题，精准助力大学生就业",
						avatar: "https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/1.png",
						note: '2022届高校毕业生规模预计达...',
						pub_at: "2023-04-19",
						source: 'XX网路有限公司招聘'
					},
					{
						id: "2",
						title: "浅谈就业指导对大学生就业的积极影响与作用",
						avatar: "https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/2.png",
						note: '大学生的就业问题一直是社会各界重点关...',
						source: 'XX网路有限公司招聘',
						pub_at: "2023-06-29"
					},
					{
						id: "3",
						title: "新手如何从零起步创业",
						avatar: "https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/3.png",
						note: '创业者必读的创业经验...',
						source: 'XX网路有限公司招聘',
						pub_at: "2023-05-09"
					},
					{
						id: "4",
						title: "招聘经验心得分享",
						avatar: "https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/1.png",
						note: '这就要提到招聘文案的重要性...',
						source: 'XX网路有限公司招聘',
						pub_at: "2023-07-11"
					}
				]

			}
		},
		onLoad() {
			uni.showTabBar()
			//设置下方的Menus菜单，才能够让发送给朋友与分享到朋友圈两个按钮可以点击
			wx.showShareMenu({
				withShareTicket: true,
				menus: ["shareAppMessage", "shareTimeline"]
			})
		},
		//发送给朋友
		onShareAppMessage(res) {
			return {
				title: '财子校园小程序',
				path: '/pages/index/index'
			}
		},
		//分享到朋友圈
		onShareTimeline(res) {
			return {
				title: '财子校园小程序',
				type: 1,
				query: 0,
				summary: "这是一款专为大学生服务的小程序，提供课表查询推送、就业招聘信息资讯、成绩查询服务等",
				imageUrl: "https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/jycy.jpg"
			}
		},
		methods: {
			//判断点击哪个功能模块
			change(e) {
				let {
					index
				} = e.detail
				this.list[index].badge && this.list[index].badge++
				uni.showToast({
					title: `点击第${index+1}个宫格`,
					icon: 'none'
				})
				if (index == 0) {
					uni.switchTab({
						url: '/pages/course/course',
					})
				} else if (index == 2) {
					uni.navigateTo({
						url: '/pages/todayCourse/todayCourse',
					})
				} else if (index == 3) {
					uni.switchTab({
						url: '/pages/guide/guide',
					})
				}
			},
			//查询成绩入口
			cxcj() {
				uni.navigateTo({
					url: '/pages/webContainer/webContainer?url=' + this.url
				})

			},
			//跳转详情页
			goDetail: function(e) {
				let detail = {
					id: e.id,
					title: e.title,
					source: e.source,
					avatar: e.avatar,
					note: e.note,
					pub_at: e.published_at

				};
				uni.navigateTo({
					url: '/pages/detail/detail?detailDate=' + encodeURIComponent(JSON.stringify(detail))
				});
			},


		}
	}
</script>

<style>
	.uni-margin-wrap {
		width: 100%;
	}

	.swiper {
		width: 100%;
		height: 300rpx;
	}

	.swiper-item {
		width: 100%;
		display: block;
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
	}

	.lunbo {
		width: 100%;
		height: 300rpx;
	}

	.grid-item-box {
		flex: 1;
		position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 15px 0;
	}

	.interaction {
		color: #999;
	}
    .info{
		position: relative;
	}
	.infoContent {
		position: absolute;
		top:0;
		left: 0;
		width: 100%;
		height: 110upx;
	}
</style>