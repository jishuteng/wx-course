<template>
	<view>
		<uni-search-bar placeholder="请输入关键词" bgColor="#EEEEEE" @confirm="search" />
		<uni-section title="校园招聘" type="line">
			<view style="background-color: #eee; width: 100%; height: 1rpx;"></view>
			<uni-card padding="0" spacing="0">
				<template v-slot:cover>
					<view class="custom-cover" @click="goHotDetail">
						<image class="cover-image" mode="aspectFill" :src="xyzp">
						</image>
						<view class="cover-content">
							<text class="uni-subtitle uni-white">最新招聘信息</text>
						</view>
					</view>
				</template>
				<uni-list>
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
				</uni-list>
			</uni-card>
		</uni-section>
		<uni-load-more status="more" />
		<!-- <uv-divider text="已经到底了"></uv-divider> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				//卡片式列表
				cover: 'https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/jycy.jpg',
				xyzp: 'https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/xyzp.png',
				avatar: '',
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
				],
			}
		},
		onLoad() {
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
				path: '/pages/guide/guide'
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
			search(res) {
				uni.showToast({
					title: '搜索：' + res.value,
					icon: 'none'
				})
			},
			//跳转到最新信息页面
			goHotDetail() {
				uni.navigateTo({
					url: '/pages/goHotDetail/goHotDetail'
				})
			},
			//跳转到校园招聘详情页
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
	.custom-cover {
		position: relative;
		width: 100%;
		height: 140px;
	}

	.cover-image {
		width: 100%;
		height: 240px;
		position: absolute;
		top: 0;
		left: 0;
		border: 0rem;

	}

	.cover-content {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		height: 40px;
		background-color: rgba(0, 0, 0, .4);
		display: flex;
		flex-direction: row;
		align-items: center;
		padding-left: 15px;
		font-size: 14px;
		color: #fff;
	}

	.info {
		position: relative;
	}

	.infoContent {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 110upx;
	}

	.carceerdInfo {
		position: relative;
	}

	.carceerdMoreIcon {
		position: absolute;
		bottom: 22%;
		right: 5%;
		margin-bottom: 12upx;
		font-size: 14px;
		color: #666;
	}
</style>