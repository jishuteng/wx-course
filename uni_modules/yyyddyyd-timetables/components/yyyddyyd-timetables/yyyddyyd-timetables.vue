<template>
	<view class="">
		<view class="" style="position:relative;left:0px;top:0px;">
			<view class="uni-search-box">
				<uni-collapse @change="changecollapse">
					<uni-collapse-item ref="collapse" :disabled="disabledcollapse" :show-arrow="false">
						<template v-slot:title>
							<view style="margin-bottom: -36px;margin-left: 10px;margin-top: 11px">
								<view @click="openpopup">
									<uni-icons size="18" type="bars" />
								</view>
							</view>

							<view @click="cesdd"
								style="margin-top: -10px;margin-left: 55px;display: flex;align-items: center;justify-content: center;height: 45px;margin-right: 26px;">
								<view class="" v-if="ckjxweek==nowjxweek">
									<text>第{{ckjxweek}}周</text>
								</view>
								<view style="color: #FF0000" v-else>
									<text>第{{ckjxweek}}周(非本周)</text>
								</view>
								<view
									:class="{ 'uni-collapse-item__title-arrow-active': isOpen, 'uni-collapse-item--animation': showAnimation === true }"
									class="uni-collapse-item__title-arrow">
									<uni-icons color="#bbb" size="14" type="bottom" />
								</view>
							</view>
							<view
								style="margin-top: -16px;font-size: 12px;transform: scale(0.5);display: flex;align-items: center;justify-content: center;">
								<text>{{xq}}</text>
							</view>
						</template>

						<view style="display: flex;background-color: #dddddd;">
							<picker mode="selector" :range="range" @change="revisenowjxweek" :value="nowjxweek"
								style="width: 10%;">
								<view class="content" style="margin-top: 3px;">
									<uni-icons type="compose" size="20">
									</uni-icons>
								</view>
								<view class="content" style="font-size: 12px;transform: scale(0.8);margin-top: -4px;">
									<text>修改</text>
								</view>
								<view class="content" style="font-size: 12px;transform: scale(0.8);margin-top: -6px;">
									<text>当前周</text>
								</view>
							</picker>
							<view style="width: 90%;background-color: #bbccdd;">
								<scroll-view :scroll-x="true" :show-scrollbar="true"
									:scroll-into-view="'week'+nowjxweek" style="white-space: nowrap;">
									<view v-for="(item,index) in jxweeksl" @click="seeweek(index+1)" :id="'week'+item"
										style="display: inline-block;border-radius: 3px;border-style: groove;border-color:#ffffff;border-width: 1px;margin: 2px;">
										<view v-if="nowjxweek==item"
											:style="ckjxweek==item?'background-color: #ffffff;height: 50px;':''">
											<view style="width: 40px;height: 50px;" class="content">
												<view style="transform: scale(0.6);font-size: 12px;">
													<text>第</text>
												</view>
												<view class="">
													<text>{{item}}</text>
												</view>
												<view style="transform: scale(0.6);font-size: 12px;">
													<text>周</text>
												</view>
											</view>
											<view class="content"
												style="position: absolute;top:35px;transform: scale(0.5);font-size: 12px; width: 40px ;">
												<text>(本周)</text>
											</view>
										</view>
										<view v-else>
											<view :style="ckjxweek==item?'background-color: #ffffff;height: 50px;':''">
												<view style="width: 40px;height: 50px;" class="content">
													<view style="transform: scale(0.6);font-size: 12px;">
														<text>第</text>
													</view>
													<view class="">
														<text>{{item}}</text>
													</view>
													<view style="transform: scale(0.6);font-size: 12px;">
														<text>周</text>
													</view>
												</view>
											</view>
										</view>
									</view>

								</scroll-view>
							</view>
						</view>
					</uni-collapse-item>
				</uni-collapse>
			</view>
		</view>
		<view class="" style="position:relative;left:0px;top:0px;">
			<uni-row class="demo-uni-row">
				<uni-col :span="3">
					<view class="demo-uni-col dark_deep"
						style="background-color: #FF7F50;display: flex;flex-direction: column;align-items: center;justify-content: center;">
						<view style="font-size: 12px;margin-right: -25rpx;">
							<text>日期</text>
						</view>
						<view style="font-size: 12px;margin-left: -25rpx;">
							<text>节数</text>
						</view>

					</view>
				</uni-col>
				<uni-col v-for="(item,index) in nowgetDates" :span="3">
					<view class="demo-uni-col dark_deep"
						style="display: flex;flex-direction: column;align-items: center;justify-content: center;"
						:style="nowriqi==item?nowweekclass:''">
						<view style="margin-top: -5px;">
							<text style="font-size: 8px;" v-if="index==0">星期日</text>
							<text style="font-size: 8px;" v-if="index==1">星期一</text>
							<text style="font-size: 8px;" v-if="index==2">星期二</text>
							<text style="font-size: 8px;" v-if="index==3">星期三</text>
							<text style="font-size: 8px;" v-if="index==4">星期四</text>
							<text style="font-size: 8px;" v-if="index==5">星期五</text>
							<text style="font-size: 8px;" v-if="index==6">星期六</text>
						</view>
						<view style="margin-top: -5px;font-size: 8px;transform: scale(0.5)">
							<text style="">{{item}}</text>
						</view>
					</view>
				</uni-col>
			</uni-row>
			<uni-row v-for="(item,index) in kbJs" class="demo-uni-row">
				<uni-col :span="3">
					<view class="demo-uni-col-shu" :style="item.style+';height:'+kbjsheight+'px'">
						<text style="font-size: 8px;">{{item.kssj}}</text>
						<text style="font-size: 8px;width: 30px;text-align: center;">{{index+1}}</text>
						<text style="font-size: 8px;">{{item.jssj}}</text>
					</view>
				</uni-col>
			</uni-row>
			<view v-for="(item,index) in nowjcweekList">
				<view v-if="item.length!=0">
					<view v-for="(a,b) in item">
						<view class="keb" @click="clickkb(a.id,index,a.jc)"
							:style="'position: absolute;top: '+((a.jc[0]-1)*78+35)+'px;left:'+(93.75*(index+1))+'rpx;height:'+(a.jc[1]-a.jc[0]+1)*78+'px;'">
							<view class="demo-uni-col-kb"
								:style="a.color?('background-color: '+a.color+';border: 1px '+a.color+' solid;'):((index+1)*(b+1))%7==0?'background-color: #aaa9bf;border: 1px #aaa9bf solid;':((index+1)*(b+1))%7==1?'background-color: #00a9bf;border: 1px #00a9bf solid;':((index+1)*(b+1))%7==2?'background-color: #9900bf;border: 1px #9900bf solid;':((index+1)*(b+1))%7==3?'background-color: #99a900;border: 1px #99a900 solid;':((index+1)*(b+1))%7==4?'background-color: #aaccbb;border: 1px #aaccbb solid;':((index+1)*(b+1))%7==5?'background-color: #44bb44;border: 1px #44bb44 solid;':((index+1)*(b+1))%7==6?'background-color: #11dddd;border: 1px #11dddd solid;':'background-color: #999999;border: 1px #999999 solid;'">
								<view :style="'height:'+(a.jc[1]-a.jc[0]+1)*74+'px;'">
									<view style="color: #F3F4F6;font-size: 20rpx;display: flex;flex-direction: column;">
										<text style="padding: 2px;">{{a.kcmc}}</text>
										<text style="padding: 2px;">{{a.kcxz}}</text>
										<view style="flex-direction: row;">
											<text style="padding: 2px;">{{a.jxdd}}</text>
											<uni-icons type="location" size="8">
											</uni-icons>
										</view>
										<text style="padding: 2px;">{{a.jsxx}}</text>
									</view>
								</view>
							</view>

						</view>
					</view>
				</view>
			</view>

		</view>
		<uni-popup ref="popup" type="bottom">
			<slot name="popup">
			</slot>
		</uni-popup>
	</view>

</template>
<script>
	const timetableapi = require("../../uniCloud/cloudfunctions/yyyddyydapi/index.js")
	//请根据官方文档配置此处信息
	var new_Date = new Date();
	var timesStamp = new_Date.getTime();
	var currenDay = new_Date.getDay();
	export default {
		props: {
			kbjsheight: {
				type: Number,
				default: 78,

			},
			range: {
				type: Array,
				default: () => ['假期中', '第1周', '第2周', '第3周', '第4周', '第5周', '第6周', '第7周', '第8周', '第9周', '第10周', '第11周',
					'第12周',
					'第13周', '第14周', '第15周', '第16周', '第17周', '第18周', '第19周', '第20周', '第21周', '第22周', '第23周', '第24周',
					'第25周',
				]
			},
			jxweeksl: { //标题
				type: Array,
				default: () => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25]
			},
			kbJs: [Array],
			kbList: [Array],
			nowweekclass: {
				type: String,
				default: 'background-color: #00FF00;'
			},
			hqxq: {
				type: String
			}
		},
		data() {
			return {
				nowgetDates: [],
				keyword: "",
				nowriqi: '',
				nowjcweekList: [],
				isOpen: false,
				showAnimation: true,
				ckjxweek: 1,
				nowjxweek: 1,
				xq: '大一第一学期',
				disabledcollapse: true,
			}
		},
		created() {
			this.nowgetDates = timetableapi.getDates(this.ckjxweek, this.nowjxweek);
			let nowriqi = new Date()
			var riqihb = (nowriqi.getMonth() + 1) + '月' + nowriqi.getDate() + '日';
			this.nowriqi = riqihb;
		},
		mounted() {
			const nowjxweek = uni.getStorageSync('yyyddyyd-timetables_nowjxweek');
			//判断当前是否有该存储值
			if (nowjxweek.setjxweektime) {
				//读取存储对象对应的值
				this.nowjxweek = timetableapi.weekgap(nowjxweek.setjxweektime) + nowjxweek.setjxweek
				this.ckjxweek = this.nowjxweek
				
			}
			this.londkb()
		},
		updated() {
			
		},
		watch: {
			kbList(newV, oldV) {
				// do something
				this.londkb()
			},
			hqxq(newV, oldV) {
				// do something
				this.xq = newV
			}
		},
		methods: {
			cesdd() {
				this.disabledcollapse = false
				setTimeout(() => {
					this.disabledcollapse = true
				}, 1000)
			},
			openpopup() {
				this.$refs.popup.open()
			},
			seeweek(e) {
				this.ckjxweek = e
				this.londkb()
				this.nowgetDates = timetableapi.getDates(this.ckjxweek, this.nowjxweek)
			},
			londkb(){
				this.nowjcweekList = timetableapi.londkb(this.kbList,this.ckjxweek);
			},
			changecollapse() {
				this.isOpen = !this.isOpen
			},
			revisenowjxweek(e) {
				this.nowjxweek = Number(e.detail.value)
				this.ckjxweek = this.nowjxweek
				uni.setStorage({
					key: 'yyyddyyd-timetables_nowjxweek',
					data: {
						setjxweek: this.nowjxweek,
						setjxweektime: timesStamp
					}
				});
				const value = uni.getStorageSync('yyyddyyd-timetables_nowjxweek');
				//判断当前是否有该存储值
				if (value) {
					//读取存储对象对应的值
				}
				this.londkb()
				this.nowgetDates = timetableapi.getDates(this.ckjxweek, this.nowjxweek)
			},
			clickkb(e, index, jc) {
				this.$emit('clickkbdata', {
					index: e,
					week: index,
					jc: jc,
					ckjxweek: this.ckjxweek
				});
			}
		}
	}
</script>
<style scoped lang="scss">
	.content {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.demo-uni-row {
		/* QQ、字节小程序文档写有 :host，但实测不生效 */
		/* 百度小程序没有 :host，需要设置block */
		/* #ifdef MP-TOUTIAO || MP-QQ || MP-BAIDU */
		display: block;
		/* #endif */
	}
	/* 支付宝小程序没有 demo-uni-row 层级 */
	/* 微信小程序使用了虚拟化节点，没有 demo-uni-row 层级 */
	/* #ifdef MP-ALIPAY || MP-WEIXIN */
	::v-deep .uni-row {
		margin-bottom: 10px;
	}
	/* #endif */
	.demo-uni-col-kb {
		margin: 5rpx 2rpx 0rpx 2rpx;
		box-shadow: 5px 5px 10px gray;
		border-radius: 4px;
		/* 标准的语法（必须放在最后） */
	}
	.demo-uni-col {
		height: 36px;
		border-radius: 4px;
	}
	.demo-uni-col-shu {
		border-radius: 4px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.keb {
		border-radius: 25px;
		width: 12.5%;
	}
	.dark_deep {
		background-color: #99a9bf;
	}
	.dark {
		background-color: #d3dce6;
	}
	.light {
		background-color: #e5e9f2;
	}
	.uni-collapse-item {
		/* #ifndef APP-NVUE */
		box-sizing: border-box;
		/* #endif */
		&__title {
			/* #ifndef APP-NVUE */
			display: flex;
			width: 100%;
			box-sizing: border-box;
			/* #endif */
			flex-direction: row;
			align-items: center;
			transition: border-bottom-color .3s;
			&-wrap {
				width: 100%;
				flex: 1;
			}
			&-box {
				padding: 0 15px;
				/* #ifndef APP-NVUE */
				display: flex;
				width: 100%;
				box-sizing: border-box;
				/* #endif */
				flex-direction: row;
				justify-content: space-between;
				align-items: center;
				height: 48px;
				line-height: 48px;
				background-color: #fff;
				color: #303133;
				font-size: 13px;
				font-weight: 500;
				/* #ifdef H5 */
				cursor: pointer;
				outline: none;
				/* #endif */
				&.is-disabled {
					.uni-collapse-item__title-text {
						color: #999;
					}
				}
			}
			&.uni-collapse-item-border {
				border-bottom: 1px solid #ebeef5;
			}
			&.is-open {
				border-bottom-color: transparent;
			}
			&-img {
				height: 22px;
				width: 22px;
				margin-right: 10px;
			}
			&-text {
				flex: 1;
				font-size: 14px;
				/* #ifndef APP-NVUE */
				white-space: nowrap;
				color: inherit;
				/* #endif */
				/* #ifdef APP-NVUE */
				lines: 1;
				/* #endif */
				overflow: hidden;
				text-overflow: ellipsis;
			}
			&-arrow {
				/* #ifndef APP-NVUE */
				display: flex;
				box-sizing: border-box;
				/* #endif */
				align-items: center;
				justify-content: center;
				width: 20px;
				height: 20px;
				margin-right: 10px;
				transform: rotate(0deg);
				&-active {
					transform: rotate(-180deg);
				}
			}
		}
		&__wrap {
			/* #ifndef APP-NVUE */
			will-change: height;
			box-sizing: border-box;
			/* #endif */
			background-color: #fff;
			overflow: hidden;
			position: relative;
			height: 0;
			&.is--transition {
				// transition: all 0.3s;
				transition-property: height, border-bottom-width;
				transition-duration: 0.3s;
				/* #ifndef APP-NVUE */
				will-change: height;
				/* #endif */
			}
			&-content {
				position: absolute;
				font-size: 13px;
				color: #303133;
				// transition: height 0.3s;
				border-bottom-color: transparent;
				border-bottom-style: solid;
				border-bottom-width: 0;
				&.uni-collapse-item--border {
					border-bottom-width: 1px;
					border-bottom-color: red;
					border-bottom-color: #ebeef5;
				}
				&.open {
					position: relative;
				}
			}
		}
		&--animation {
			transition-property: transform;
			transition-duration: 0.3s;
			transition-timing-function: ease;
		}
	}
</style>
