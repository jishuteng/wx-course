<template>
	<view class="container" style="background-color: #F8F8F8;">
		<uni-card title="心善志坚" :isFull="true" sub-title="ID:3691468257" :thumbnail="avatar">
			<text class="uni-body">座右铭：生命不息，奋斗不止，不辜负青春，不辜负韶华</text>
		</uni-card>
		<view class="list-cell b-b m-t" @click="navTo('个人资料')" hover-class="cell-hover" :hover-stay-time="50">
			<text class="cell-tit">个人资料</text>
			<text class="cell-more yticon icon-you">完善资料</text>
			<uni-icons type="arrowright" color="#C9C9C9" size="20"></uni-icons>
		</view>
		<view class="list-cell" @click="verifyStudent" hover-class="cell-hover" :hover-stay-time="50">
			<text class="cell-tit">学生认证</text>
			<uni-icons type="arrowright" color="#C9C9C9" size="20"></uni-icons>
		</view>
		<view class="list-cell m-t b-b" @click="clearStorage" hover-class="cell-hover" :hover-stay-time="50">
			<text class="cell-tit">清除缓存</text>
			<text class="cell-more yticon icon-you">{{storageSize}}</text>
			<uni-icons type="arrowright" color="#C9C9C9" size="20"></uni-icons>
		</view>
		<view class="list-cell b-b" @click="navTo('关于Dcloud')" hover-class="cell-hover" :hover-stay-time="50">
			<text class="cell-tit">帮助文档</text>
			<text class="cell-more yticon icon-you"></text>
			<uni-icons type="arrowright" color="#C9C9C9" size="20"></uni-icons>
		</view>
		<view class="list-cell" @click="checkUpdate">
			<text class="cell-tit">检查更新</text>
			<text class="cell-tip">当前版本 1.0.3</text>
			<uni-icons type="arrowright" color="#C9C9C9" size="20"></uni-icons>
		</view>
		<view class="list-cell log-out-btn" @click="toLogout">
			<text class="cell-tit">退出登录</text>
		</view>
	</view>
</template>

<script>
	import {
		mapMutations
	} from 'vuex';
	export default {
		data() {
			return {
				avatar: 'https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/avatar.png',
				storageSize: '0M',
			};
		},
		onLoad() {
			//获取缓存
			this.getStorageSize()
		},
		methods: {
			...mapMutations(['logout']),

			navTo(url) {
				this.$api.msg(`跳转到${url}`);
			},
			//学生认证
			verifyStudent() {
				uni.navigateTo({
					url: '/pages/verifyStudent/verifyStudent',
				})
			},
			//获取app的缓存
			getStorageSize: function() {
				
			},
			//删除 缓存
			clearStorage: function() {
			},
			checkUpdate(){
				
			},
			//退出登录
			toLogout() {
				uni.showModal({
					content: '确定要退出登录么',
					success: (e) => {
						if (e.confirm) {
							uni.navigateTo({
								url:'/pages/login/login'
							})
						}
					}
				});
			},

		}
	}
</script>

<style lang='scss'>
	page {
		background: $page-color-base;
	}

	.list-cell {
		display: flex;
		align-items: baseline;
		padding: 20upx $page-row-spacing;
		line-height: 60upx;
		position: relative;
		background: #fff;
		justify-content: center;
		box-shadow: 0px 0px 3px 1px rgba(0, 0, 0, 0.08);

		&.log-out-btn {
			margin-top: 40upx;

			.cell-tit {
				color: $uni-color-primary;
				text-align: center;
				margin-right: 0;
			}
		}

		&.cell-hover {
			background: #fafafa;
		}

		&.b-b:after {
			left: 30upx;
		}

		&.m-t {
			margin-top: 16upx;
		}

		.cell-more {
			align-self: baseline;
			font-size: $font-lg;
			color: $font-color-light;
			margin-left: 10upx;
		}

		.cell-tit {
			flex: 1;
			font-size: $font-base + 2upx;
			color: $font-color-dark;
			margin-right: 10upx;
		}

		.cell-tip {
			font-size: $font-base;
			color: $font-color-light;
		}

		.shareBtn {
			border: 0px;
			background-color: #fff;

		}
	}
</style>