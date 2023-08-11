<template>
	<view class="container">
		<uni-section title="信息均为必填" type="line">
			<view class="course">
				<!-- 自定义表单校验 -->
				<uni-forms ref="customForm" :rules="customRules" :modelValue="customFormData">
					<uni-forms-item label="课程" required name="course">
						<uni-easyinput v-model="customFormData.course" placeholder="请输入课程名" />
					</uni-forms-item>
					<uni-forms-item label="老师" required name="teacher">
						<uni-easyinput v-model="customFormData.teacher" placeholder="请输入上课老师" />
					</uni-forms-item>
					<uni-forms-item label="教室" required name="classroom">
						<uni-easyinput v-model="customFormData.classroom" placeholder="请输入上课地点" />
					</uni-forms-item>
					<uni-forms-item label="时间" required >
						<uni-data-picker placeholder="请选择地址" popup-title="请选择城市" @change="onchange" :range="timeList" :value="timesIndex">
							<picker   mode="multiSelector" :range="timeList" :value="timesIndex" @change="bindTimeChange">
								<view>
									{{timeList[0][timesIndex[0]]}}:{{timeList[1][timesIndex[1]]}}:{{timeList[1][timesIndex[1]]}}
								</view>
							</picker>
						</uni-data-picker>
					</uni-forms-item>
					<uni-card :is-shadow="false" is-full>
						<view style="text-align: left;font-size: 14px;">勾选上课周次</view>
					</uni-card>
					<view style="margin: 20upx 0;width: 100%;"></view>
					<uni-forms-item label="" name="weektime" style="margin-left: 40upx;font-size: 16px;">
						<uni-data-checkbox v-model="customFormData.weektime" multiple :localdata="weektimes" />	
					</uni-forms-item>
				</uni-forms>
				<button type="default" @click="submit('customForm')" style="background-color: #1296db;color: #fff;">保存</button>
			</view>
		</uni-section>
		<view class="tab-bar">
			<view v-for="(item,index) in list" :key="index" class="tab-bar-item" @click="switchTab(item, index)">
				<image class="tab_img" :src="selected === index ? item.selectedIconPath : item.iconPath"></image>
				<view class="tab_text" :style="{color: selected === index ? selectedColor : color}">{{item.text}}
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		props: {
			// 当前选中的tab index
			selected: {
				type: Number,
				default: 0
			},
		},
		data() {
			return {
				timeList: [['星期','02','03','04','05','06','07','08','09','10'],['开始时间','10','20','30','40','50','60'],['结束时间','10','20','30','40','50','60']],
				timesIndex: [0,0,0],

				// 自定义表单数据
				customFormData: {
					course: '',
					teacher: '',
					classroom: '',
					weektime: [],
					datetimesingle: 1627529992399

				},
				// 自定义表单校验规则
				customRules: {
					course: {
						rules: [{
							required: true,
							errorMessage: '课程名不能为空'
						}]
					},
					teacher: {
						rules: [{
							required: true,
							errorMessage: '上课老师不能为空'
						}]
					},
					classroom: {
						rules: [{
							required: true,
							errorMessage: '上课地点不能为空'
						}]
					},
					weektime: {
						rules: [{
								format: 'array'
							},
							{
								validateFunction: function(rule, value, data, callback) {
									if (value.length < 1) {
										callback('请至少勾选一项周次')
									}
									return true
								}
							}
						]
					}

				},
			}
		},
		onLoad() {},
		onReady() {
			// 设置自定义表单校验规则，必须在节点渲染完毕后执行
			this.$refs.customForm.setRules(this.customRules)
		},
		methods: {
			bindTimeChange(e){
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.timesIndex = e.target.value
				},

			
			//周次调用函数
			onnodeclick(e) {
				console.log(e);
			},
			onpopupopened(e) {
				console.log('popupopened');
			},
			onpopupclosed(e) {
				console.log('popupclosed');
			},
			onchange(e) {
				console.log('onchange:', e);
			},


			onClickItem(e) {
				console.log(e);
				this.current = e.currentIndex
			},
			submit(ref) {
				this.$refs[ref].validate().then(res => {
					console.log('success', res);
					uni.showToast({
						title: `校验通过`
					})
				}).catch(err => {
					console.log('err', err);
				})
			},
		}
	}
</script>
<style>
	.course {
		padding: 15px;
		background-color: #fff;
	}

	.segmented-control {
		margin-bottom: 15px;
	}

	.button-group {
		margin-top: 15px;
		display: flex;
		justify-content: space-around;
	}

	.form-item {
		display: flex;
		align-items: center;
	}

	.button {
		width: 30upx;
		display: flex;
		align-items: center;
		height: 35px;
		margin-left: 10px;
	}

</style>