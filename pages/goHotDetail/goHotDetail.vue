<template>
	<view>
		<view class="uni-box-head">
			<uni-title type="h3" align="center" title="最新招聘就业信息"></uni-title>
		</view>
		<uni-row class="nav-title" :width="nvueWidth">
			<uni-col :span="10">
				<view class="text-sty">日期：2023-07-09</view>
			</uni-col>
			<uni-col :span="14">
				<view class="text-sty">来源：XXX官方网站</view>
			</uni-col>
		</uni-row>
		<view class="thumb">
			<image class="banner-img" :src="avatar"></image>
		</view>
		<!-- 内容详情页 -->
		<view class="article-content">
			<uni-row class="demo-uni-row" :width="nvueWidth">
				<uni-col>
					<view class="demo-uni-col dark_deep">软件工程师10000元以上/月</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">招聘单位：中泰元科股份有限公司学历要求：</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">面议发布机构：山西省人力资源市场</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">工作性质：均可</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">工作地点：山西省/太原市/阳曲县</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">研发职位性质：全职</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">工作地点：北京市海淀区、西安</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">学历要求：大学本科以上学历</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">招聘人数：若干</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">接受应聘邮件的电子邮箱：hr@powerscan.com.cn</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">岗位职责：</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">1、系统业务流程及数据管理软件的设计、开发及测试。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">2、用户应用软件的设计、开发及测试。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">3、技术文档及手册的编制与整理。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">任职要求：</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">1、大学本科及以上学历，计算机、电子、自动化、仪器及相关专业。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">2、应届毕业生或在职均可。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">3、一年以上C/C++项目开发经验，具有良好的编程基础和编程风格，熟悉面向对象的设计方法，熟悉VC开发环境。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">4、有软件工程基础，熟悉.NET平台、熟悉数据库，有Windows应用程序的设计开发经验者优先。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">5、良好的团队精神和沟通能力，较好的文字表达能力，有编写实际软件产品使用手册经验的优先。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">6、良好的英文阅读、理解、文字表达能力。</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">联 系 人 ：姚影</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">联 系 电 话：13301076026</view>
				</uni-col>
				<uni-col>
					<view class="demo-uni-col dark_deep">邮 箱：hr@powerscan.com.cn</view>
				</uni-col>
			</uni-row>	
		</view>
		<!-- 分割线 -->
		<view style="display: flex;margin-top:5rpx ;">
			<view style="background-color: lightgray; width: 100%; height: 1rpx;"></view>
		</view>
		<!-- 底部互动内容 -->
		<view class="interaction">
			<uni-row :width="nvueWidth">
				<uni-col :span="8">
					<view>阅读数:345</view>
				</uni-col>
				<uni-col :span="8">
					<view class="interacte-sty">
						<image src="https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/share.png" style="width: 16px;height: 16px;"
							class="shareIcon">分享</image>
						<button open-type="share" class="shareBtn"></button>

					</view>
				</uni-col>
				<uni-col :span="8">
					<view>点赞<uni-icons type="hand-up" size="20"></uni-icons></view>
				</uni-col>
			</uni-row>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: '最新招聘就业信息',
				avatar:'https://mp-7b604e11-5098-4a9b-880c-4658d63b9294.cdn.bspapp.com/images/xyzp.png'
			}
		},
		onLoad(event) {
			//获取上一页传过来的参数
			/* this.banner = JSON.parse(decodeURIComponent(event.detailDate)); */
			//详情标题
			uni.setNavigationBarTitle({
				title: "最新招聘就业信息",
			});
			
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
			
		}
	}
</script>
<style lang="scss">
	.text-sty {
		color: #999;
		padding-left: 10%;
		font-size: 14px;
	}

	.thumb {
		margin-top: 20upx;
	}

	.banner-img {
		width: 90%;
		margin-left: 5%;
		border-radius: 2% 2% 2% 2%;
	}

	.article-content {
		padding-left: 5%;
		padding-right: 5%;
		padding-top: 5%;
		padding-bottom: 5%;
		color: #333;
	}

	.interaction {
		color: #666;
		padding-left: 5%;
		margin-top: 5%;
		padding-bottom: 5%;
	}

	.interacte-sty {
		position: relative;
	}

	.shareIcon {
		position: absolute;
		top: 0upx;
		left: 70upx;
	}

	.shareBtn {
		position: absolute;
		top: 0;
		left: -30upx;
		width: 60%;
		height: 100%;
		opacity: 0;
	}

	.shareContent {
		position: absolute;
		top: 0;
		left: 20upx;
	}
</style>