<template>
	<view class="container">
		<view class="top-pic">
			<view class="text1">
				<text> 豫见山海 </text>
			</view>
			<view class="text2">
				<text> 躬行以践，奔赴山海 </text>
			</view>
			<image class="pic" src="https://rashawn.oss-cn-shanghai.aliyuncs.com/img/blueberry.png"> </image>
		</view>
	
		<view class="info">
			<swiper autoplay="true" :interval="interval">
				<swiper-item v-for="(item, index) in texts" :key="index">
					<view class="info-text">
						<text> {{item}} </text>
					</view>		
				</swiper-item>
			</swiper>
		</view>
		
		<view class="product-box1" @click="onclick(1)">
			<view class="text3">
				<text> 项目介绍 </text>
			</view>
<!-- 			<view class="text4">
				<text> 成果简介 </text>
			</view> -->
		</view>
		
		<view class="product-box2" @click="onclick(2)"> 
			<view class="text5">
				<text> 实践成果 </text>
			</view>
		</view>
		
		<view class="show-text">
			<text> 数据展示 </text>
		</view>
		
		<view class="stats1">
			<view class="data-show">
				<text class="title_1">发展趋势</text>
			</view>
			<image class="data-pic" @tap="previewImage(0)" src="https://rashawn.oss-cn-shanghai.aliyuncs.com/img/graph1.png" mode="scaleToFill"></image>
		</view>
		
		<view class="stats2">
			<view class="data-show">
				<text class="title_1">关联产业</text>
			</view>
			<image class="data-pic" @tap="previewImage(1)" src="https://rashawn.oss-cn-shanghai.aliyuncs.com/img/graph2.jpeg" mode="widthFix"></image>
		</view>
		
		<text class="ref">
			图片来自：云果网：2022年中国蓝莓产业数据分析报
		</text>
	</view>
</template>
<script>
	// import 'viewerjs/dist/viewer.css'
	// import Viewer from 'v-viewer'

	export default {
		data() {
			return {
				texts: ["习近平总书记在党的二十大报告中指出，“发展乡村特色产业，拓宽农民增收致富渠道。巩固拓展脱贫攻坚成果，增强脱贫地区和脱贫群众内生发展动力。”产业振兴助力乡村振兴，仍是建设新时代农业强国的重要课题。",
						"作为2020年成功摘掉国家级贫困县帽子的河南省鲁山县，其所辖的库区乡于2012年开始走上发展蓝莓产业的道路，经过十多年种植摸索，已经成为“中原蓝莓第一乡”。可以说，在该县的脱贫攻坚战中，小小蓝莓发挥了巨大作用。",
						"来自南京大学”豫见山海“社会实践团队的同学们在暑假期间，来到河南省鲁山县东许庄村，实地走访当地村民、村干部、企业工作人员、高校研究人员，探究”小小蓝精灵，铺就致富路“背后的秘密，亲身体会乡村振兴的生机活力。",
						],
				link: "https://mp.weixin.qq.com/s/l2LcRhWVK_IuVHnOq4WZWA",
				pic: [
					"https://rashawn.oss-cn-shanghai.aliyuncs.com/img/graph1.png",
					"https://rashawn.oss-cn-shanghai.aliyuncs.com/img/graph2.jpeg"
				],
				interval: 8000,
				// pageIndex: 1,
				// loadding: false,
				// pullUpOn: true,
				// opacity: 1
			};
		},
		methods: {
			onclick: function(idx){
				uni.navigateTo({
					url: '/pages/component/detail/detail' + idx
				});
			},
			
			previewImage:function(index){
				console.log(index)
				wx.previewImage({
				  current: this.pic[index], // 当前显示图片的http链接
				  urls: [this.pic[index]], // 需要预览的图片http链接列表  ===重中之重===
				})
			}
		},
		onPullDownRefresh: function() {
			let loadData = JSON.parse(JSON.stringify(this.productList));
			loadData = loadData.splice(0, 10);
			this.productList = loadData;
			this.pageIndex = 1;
			this.pullUpOn = true;
			this.loadding = false;
			uni.stopPullDownRefresh();
		},
		onReachBottom: function() {
			if (!this.pullUpOn) return;
			this.loadding = true;
			if (this.pageIndex == 4) {
				this.loadding = false;
				this.pullUpOn = false;
			} else {
				let loadData = JSON.parse(JSON.stringify(this.productList));
				loadData = loadData.splice(0, 10);
				if (this.pageIndex == 1) {
					loadData = loadData.reverse();
				}
				this.productList = this.productList.concat(loadData);
				this.pageIndex = this.pageIndex + 1;
				this.loadding = false;
			}
		},
		onPageScroll(e) {
			// #ifdef APP-PLUS
			let scrollTop = e.scrollTop;
			if (scrollTop < 0) {
				if (this.opacity > 0)
					this.opacity = 1 - Math.abs(scrollTop) / 30;
			} else {
				this.opacity = 1
			}
			// #endif
		}
	};
</script>

<style>
	.top-pic{
		left: 0px;
		top: 1px;
		width: 100%;
		height: 214px;
		line-height: 20px;
		background-color: rgba(186, 231, 255, 0.5);
		text-align: center;
	}
	
	.info{
		margin-left: 5%;
		top: 154px;
		width: 90%;
		height: 157px;
		line-height: 20px;
		border-radius: 10px 10px 10px 10px;
		background-color: rgba(0, 80, 179, 1);
		color: rgba(255, 255, 255, 1.0);
		font-size: 14px;
		text-align: left;
		box-shadow: 0px 2px 6px 0px rgba(64, 169, 255, 1);
		font-family: Arial;
		position: absolute;
	}
	
	.text1{
		position: absolute;
		left: 24px;
		top: 77px;
		width: 113px;
		height: 82px;
		color: rgba(16, 16, 16, 1);
		font-size: 28px;
		text-align: left;
		font-weight: bold;
		font-family: PingFangSC-regular;
	}
	
	.text2{
		position: absolute;
		left: 24px;
		top: 117px;
		width: 273px;
		height: 20px;
		color: rgba(16, 16, 16, 1);
		font-size: 14px;
		text-align: left;
		font-family: PingFangSC-regular;
	}
	
	.text3{
		position: absolute;
		top: 30px;
		width: 100%;
		height: 57px;
		color: rgba(251, 251, 251, 1);
		font-size: 20px;
		text-align: center;
		font-weight: bold;
		font-family: PingFangSC-regular;
	}
	
	.text4{
		position: absolute;
		top: 30px;
		width: 100%;
		height: 41px;
		color: rgba(251, 251, 251, 1);
		font-size: 14px;
		text-align: center;
		font-family: PingFangSC-regular;
	}
	
	.text5{
		position: absolute;
		top: 30px;
		width: 100%;
		height: 57px;
		color: rgba(251, 251, 251, 1);
		font-size: 20px;
		text-align: center;
		font-weight: bold;
		font-family: PingFangSC-regular;
	}
	
	.product-box1{
		position: absolute;
		left: 5%;
		top: 325px;
		width: 43%;
		height: 80px;
		line-height: 20px;
		border-radius: 10px;
		background-color: rgba(105, 192, 255, 1);
		text-align: center;
		box-shadow: 0px 2px 6px 0px rgba(145, 213, 255, 1);
	}
	
	.product-box2{
		position: absolute;
		right: 5%;
		top: 325px;
		width: 43%;
		height: 80px;
		line-height: 20px;
		border-radius: 10px;
		background-color: rgba(149, 222, 100, 1);
		text-align: center;
		box-shadow: 0px 2px 6px 0px rgba(217, 247, 190, 1);
	}
	
	.show-text{
		position: absolute;
		margin-left: 35%;
		padding-top: 5px;
		top: 422px;
		width: 30%;
		height: 29px;
		line-height: 23px;
		border-radius: 10px 10px 10px 10px;
		background-color: rgba(154, 154, 154, 1);
		color: rgba(255, 255, 255, 1);
		font-size: 16px;
		text-align: center;
		font-family: Arial;
	}
	
	.stats1{
		position: absolute;
		left: 5%;
		top: 470px;
		width: 90%;
		height: 248px;
		line-height: 20px;
		border-radius: 5px;
		background-color: rgba(255, 255, 255, 1);
		text-align: center;
		border: 1px solid rgba(221, 219, 219, 1);
	}
	
	.stats2{
		position: absolute;		
		left: 5%;
		top: 782px;
		width: 90%;
		height: 248px;
		line-height: 20px;
		border-radius: 5px;
		background-color: rgba(255, 255, 255, 1);
		text-align: center;
		border: 1px solid rgba(221, 219, 219, 1);
	}
	
	.ref{
		position: absolute;
		left: 5%;
		top: 1180px;
		width: 90%;
		
		color: rgba(138, 138, 138, 1.0);
		font-size: 12px;
		text-align: left;
		text-overflow: clip;
		font-family: PingFangSC-regular;
		word-wrap:break-word;
	}
	
	.info-text{
		position: absolute;
		padding-left: 20px;
		padding-right: 20px;
		top: 20px;
	}
	
	.container{
		flex: 1;
	}
	
	.pic{
		position: absolute;
		right: 0px;
		top: 15px;
		width: 194px;
		height: 194px;
		opacity: 0.75;
	}
	
	.data-show{
		top:0rpx;
		margin: 0 auto;
		width: 100%;
		height: 49px;
		background-color: rgba(124, 159, 205, 1.0)
	}
	
	.data-pic{
		width: 100%;
	}
	
	.title_1{
		position: absolute;
		margin-left:-45%;
		margin-top:15px;
		font-size: 18px;
		color: #fff;
		font-weight: bold;
	}
		
</style>
