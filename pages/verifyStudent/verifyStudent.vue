<template>
	<view>
		<view class="main-box">
			<view class="bg-one"></view>
			<view class="bg-two"></view>
			<view class="tips">
				<text class="title">学生认证</text>
				<text class="mt-2 subtitle animation-slide-top">账户密码与教务系统一致</text>
			</view>
			<form bindsubmit="login">
				<view class="form-box">
					<view class="input-box">
						<input type='number' @input="inputID" :value="yhm" placeholder="请输入学号" maxlength="20" />
					</view>
					<view class="input-box">
						<input password @input="inputPass" :value="mm" placeholder="请输入密码" maxlength="20" />
						<text class="p-4 cicon-eye-off-o" bindtap="showPass"></text>
					</view>
					<button>登录</button>
				</view>
			</form>
		</view>
		<view class="animation"></view>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				showpass: false,
				yhm: '',
				mm: '',
			}
		},
		methods: {
		}
	}
</script>

<style lang="scss">
	page {
		background-color: rgb(118, 218, 255);
	}

	.main-box {
		width: 100%;
		height: 162vw;
		margin: 0;
		padding: 0;
		position: relative;
		background-color: rgb(118, 218, 255);
		overflow: hidden;

		&::after {
			content: '';
			position: absolute;
			bottom: 15vh;
			min-width: 300vw;
			min-height: 300vw;
			left: -95%;
			border-radius: 46%;
			background-color: #FFFFFF;
			-webkit-animation: rote 10s linear infinite;
			animation: rote 10s linear infinite;
		}

		&::before {
			content: '';
			position: absolute;
			bottom: 15vh;
			min-width: 300vw;
			min-height: 300vw;
			left: -95%;
			border-radius: 45%;
			opacity: .5;
			background-color: #FFFFFF;
			-webkit-animation: rote 10s linear infinite;
			animation: rote 10s linear infinite;
		}

		.bg-one {
			position: fixed;
			top: -120rpx;
			right: -230rpx;
			width: 480rpx;
			height: 480rpx;
			border-radius: 100%;
			background-color: #00baef;
			z-index: 2;
		}

		.bg-two {
			position: fixed;
			top: -0rpx;
			right: -300rpx;
			width: 500rpx;
			height: 500rpx;
			border-radius: 100%;
			background-color: #ade8f9;
			z-index: 1;
		}

		.tips {
			position: relative;
			padding-top: 160rpx;
			padding-left: 80rpx;
			display: flex;
			flex-direction: column;
			z-index: 2;

			.title {
				line-height: 70rpx;
				font-weight: bold;
				font-size: 50rpx;
			}

			.subtitle {
				line-height: 70rpx;
				font-size: 35rpx;
				font-weight: bold;
				color: #b0b0b1;
			}
		}

		.form-box {
			margin-top: 100upx;
			padding: 60rpx;
			position: relative;
			z-index: 9999;

			.icon {
				font-size: 65rpx;
			}

			.name {
				margin-top: -20rpx;
			}

			.input-box {
				margin: 40rpx 0;
				display: flex;
				justify-content: flex-start;
				align-items: center;
				height: 80rpx;
				width: 100%;
				background-color: #f5f5f5;
				border-radius: 80rpx;

				text {
					font-size: 36rpx;
				}

				input {
					flex: 1;
					height: 100%;
					font-size: 30rpx;
					padding-left: 40rpx;
				}
			}

			button {
				display: flex;
				justify-content: center;
				align-items: center;
				width: 100%;
				height: 100rpx;
				border-radius: 100rpx;
				color: #FFFFFF;
				background: linear-gradient(to right, #00c6fc, #9adcf1);

				&::after {
					border: 0 !important;
				}
			}
		}
	}

	@-webkit-keyframes rote {
		from {
			-webkit-transform: rotateZ(0);
			transform: rotateZ(0);
		}

		to {
			-webkit-transform: rotateZ(360deg);
			transform: rotateZ(360deg);
		}
	}

	@keyframes rote {
		from {
			-webkit-transform: rotateZ(0);
			transform: rotateZ(0);
		}

		to {
			-webkit-transform: rotateZ(360deg);
			transform: rotateZ(360deg);
		}
	}
</style>