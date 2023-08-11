<template>
	<view>
		<ly-curriculumtable :weekTableState="true" :weekTableNumber="weekNumbers" :controlWeek="controlWeek" :timetableType="timetableType"
			:timetables="timetables" :startdDate="startdDate" :weekButton="weekButton" @nextWeekClick="nextWeekClick" @lastWeekClick="lastWeekClick"
			@courseClick="courseClick" @weekSelectClick="weekSelectClick" @weekOpenClick="weekOpenClick">
		</ly-curriculumtable>
		<view>
			<uni-fab ref="fab" :pattern="pattern" :content="content" :horizontal="horizontal" :vertical="vertical" :direction="direction"
				@trigger="trigger" @fabClick="fabClick" />
		</view>
		<!-- 课程详情 -->
		<uni-popup ref="popup" type="message">
			<uni-popup-dialog type="info" title="课程详情" mode="base" :duration="2000" :before-close="true" @close="closeModal" @confirm="confirm">
				<view class="course-content">
					<view class="divider"></view>
					<uni-row class="uni-row" :width="nvueWidth">
						<uni-col v-for="(item,index) in modalItem" :key="index" class="course-detail">
							<view :class="modalIcon[index]" class="course-icon"></view>
							<view class="course-detail">{{item}}</view>
						</uni-col>
					</uni-row>
				</view>
			</uni-popup-dialog>
		</uni-popup>
	</view>
</template>
<script>
	export default {
		components: {},
		data() {
			return {
				//底部菜单当前项
				gutter: 0,
				nvueWidth: 730,
				weekNumbers: 20, //一共显示几周
				controlWeek: 1, //显示的第几周
				weekButton: true, //开启上一周下一周按钮
				startdDate: '', //开始时间  默认为当前时间
				//获取周课表所有课程
				timetables: [
					['大学英语', '大学英语', '', '', '','毛概', '毛概','大学体育','大学体育','数字电子技术基础','数字电子技术基础','数字电子技术基础'],
					['', '','信号与系统', '信号与系统', '信号与系统','计算机网络技术', '计算机网络技术', '模拟电子技术基础', '模拟电子技术基础','信号与系统', '信号与系统', '信号与系统'],
					['大学体育', '大学体育', '形势与政策', '形势与政策', '形势与政策', '', '',  '机械设计技术基础','机械设计技术基础','','',''],
					['大学英语', '大学英语','', '','','数字电子技术基础','数字电子技术基础', '', '','数据结构与算法分析', '数据结构与算法分析','数据结构与算法分析'],
					['毛概', '毛概','数据结构与算法分析', '数据结构与算法分析', '数据结构与算法分析', '', '', '信号与系统','信号与系统','','',''],
				],
				timetableType: [
					
				    {
				    	index: '1',
				    	name: '08:00\n08:45'
				    },
				    {
				    	index: '2',
				    	name: '08:55\n09:40'
				    },
				    {
				    	index: '3',
				    	name: '09:40\n09:55'
				    },
				    {
				    	index: '4',
				    	name: '09:55\n10:40'
				    },
				    {
				    	index: '5',
				    	name: '10:50\n11:35'
				    },
				    {
				    	index: '6',
				    	name: '11:45\n12:30'
				    },
				    {
				    	index: '7',
				    	name: '12:30\n14:30'
				    },
				    {
				    	index: '8',
				    	name: '14:30\n15:15'
				    },
				    {
				    	index: '9',
				    	name: '15:25\n16:10'
				    },
				    {
				    	index: '10',
				    	name: '16:10\n16:25'
				    },
				    {
				    	index: '11',
				    	name: '16:25\n17:10'
				    },
				    {
				    	index: '12',
				    	name: '17:20\n18:05'
				    },
				    {
				    	index: '13',
				    	name: '18:05\n19:00'
				    },
				    {
				    	index: '14',
				    	name: '19:00\n19:45'
				    },
				    {
				    	index: '15',
				    	name: '19:50\n20:35'
				    },
				    {
				    	index: '16',
				    	name: '20:40\n21:25'
				    } 
				],
				//弹窗属性
				modalIcon: ['iconfont icon-kecheng', 'iconfont icon-weizhi', 'iconfont icon-laoshi', 'iconfont icon-time'], //图标
				modalItem: [], //依次是课程名、教室、教师、上课时间--为了适配渲染
				//配置悬浮按钮功能
				horizontal: 'right',
				vertical: 'bottom',
				direction: 'horizontal',
				pattern: {
					color: '#7A7E83',
					backgroundColor: '#fff',
					selectedColor: '#1296db',
					buttonColor: '#1296db',
					iconColor: '#fff'
				},
				is_color_type: true,
				content: [{
						iconPath: '/static/fab/jianchagengxin.png',
						selectedIconPath: '/static/fab/jianchagengxin-selected.png',
						text: '更新',
						active: true
					},
					{
						iconPath: '/static/fab/zidingyi.png',
						selectedIconPath: '/static/fab/zidingyi-selected.png',
						text: '自定义',
						active: false
					},
					{
						iconPath: '/static/fab/tixing.png',
						selectedIconPath: '/static/fab/tixing-selected.png',
						text: '今日',
						active: false
					},
					{
						iconPath: '/static/fab/setting.png',
						selectedIconPath: '/static/fab/setting-selected.png',
						text: '设置',
						active: false
					}
				],
			}

		},
		onLoad() {
			wx.showShareMenu({
			        withShareTicket:true,
			        //设置下方的Menus菜单，才能够让发送给朋友与分享到朋友圈两个按钮可以点击
					//"shareAppMessage"分享给朋友,"shareTimeline"分享朋友圈
			        menus:["shareAppMessage"]
			    })
		},

		onShareAppMessage(res) {
			if (res.from === 'button') { // 来自页面内分享按钮
				console.log(res.target)
			}
			return {
				title: '本学期课程表', //分享的名称
				path: '/pages/course/course',//分享后跳转的页面
				mpId: 'wxa90b4769a0516342' //此处配置微信小程序的AppId
			}
		},
		//分享到朋友圈
		onShareTimeline(res) {
			return {
				title: '本学期',
				type: 0,
				summary: "",
			}
		},

		methods: {

			//悬浮按钮功能
			trigger(e) {
				console.log(e.index)
				if (e.index === 0) {
					this.content[e.index].active = true
					uni.showToast({
						title: '数据更新成功',
						icon: 'success',
						mask: true,
						success: () => {
							setTimeout(function() {
								this.$forceUpdate;
							}, 1000);
						}
					});
				} else if (e.index === 1) {
					uni.navigateTo({
						url: '/pages/define/define',
					})
				} else if(e.index == 2 ){
					uni.navigateTo({
						url: '/pages/todayCourse/todayCourse',
					})
				}else if( e.index == 3){
					uni.navigateTo({
						url: '/pages/setCourse/setCourse',
					})
				}
			},
			fabClick() {
				uni.showToast({
					title: '点击了悬浮按钮',
					icon: 'none'
				})
			},
			courseClick(re) {
				this.modalItem[0] = "课程: " + re.name;
				this.modalItem[1] = "教室: 213"
				this.modalItem[2] = "教师: 吴老师"
				this.modalItem[3] = "时间: 9:00-9:40";
				this.$set(this.modalItem, this.modalItem)
				this.$refs.popup.open('center');

			},
			nextWeekClick(e) {
				console.log("下一周", e)
			},
			lastWeekClick(e) {
				console.log("上一周", e)
			},
			weekOpenClick() {
				console.log("点击了第几周")
			},
			weekSelectClick(e) {
				console.log("您选择了", e)
			},
			//关闭弹窗
			closeModal() {
				this.$refs.popup.close();
			},
			confirm() {
				// 输入框的值
				console.log("收到")
				
				this.$refs.popup.close()
			},
			//返回颜色
			colorList() {
				return [
					"#ffffff", //0
					"#ffaa00", //1
					"#33CC99",
					"#ff5500", //3
					"#789262", //4
					"#66CCCC", //5
					"#9999FF", //6
				]
			},

		},
	}
</script>
<style scoped lang="scss">
	.course-icon {
		float: left;
		margin-right: 10upx;
		margin-top: 10upx;
		color: chocolate;
		font-size: 16px;
		font-weight: bold;
	}

	.course-detail {
		color: #1296db;
		margin-top: 10upx;
		font-size: 16px;
	}

	.divider {
		background-color: #E0E3DA;
		width: 100%;
		height: 2upx;
	}

	.tab-bar {
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		height: 100rpx;
		background: white;
		display: flex;
		justify-content: center;
		align-items: center;
		padding-bottom: env(safe-area-inset-bottom); // 适配iphoneX的底部
	}

	.tab-bar-item {
		flex: 1;
		text-align: center;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}

	.tab_img {
		width: 37rpx;
		height: 41rpx;
	}

	.tab_text {
		font-size: 20rpx;
		margin-top: 9rpx;
	}
</style>