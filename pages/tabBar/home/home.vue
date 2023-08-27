<template>
	<view class="container">
		<view class="top-pic">
			<view class="text1">
				<text> 豫见山海 </text>
			</view>
			<view class="text2">
				<text> 躬行以践，奔赴山海 </text>
			</view>
		</view>
	
		<view class="info">
			<swiper :indicator-dots="true">
				<swiper-item v-for="(item, index) in texts" :key="index">
					<view class="info-text">
						<text> {{item}} </text>
					</view>		
				</swiper-item>
			</swiper>
		</view>
		
		<view class="product-box1" @click="onclick(1)">  
			<view class="text3">
				<text> 产业成果 I </text>
			</view>
			<view class="text4">
				<text> 成果简介 </text>
			</view>
		</view>
		
		<view class="product-box2" @click="onclick(1)"> 
			<view class="text5">
				<text> 产业成果 II </text>
			</view>
		</view>
		
		<view class="show-text">
			<text> 数据展示 </text>
		</view>
		
		<view class="stats1">
		</view>
		
		<view class="stats2">
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				texts: ["习近平总书记在党的二十大报告中指出，“发展乡村特色产业，拓宽农民增收致富渠道。巩固拓展脱贫攻坚成果，增强脱贫地区和脱贫群众内生发展动力。”产业振兴助力乡村振兴，仍是建设新时代农业强国的重要课题。",
						"作为2020年成功摘掉国家级贫困县帽子的河南省鲁山县，其所辖的库区乡于2012年开始走上发展蓝莓产业的道路，经过十多年种植摸索，已经成为“中原蓝莓第一乡”。可以说，在该县的脱贫攻坚战中，小小蓝莓发挥了巨大作用。",
						"来自南京大学”豫见山海“社会实践团队的同学们在暑假期间，来到河南省鲁山县东许庄村，实地走访当地村民、村干部、企业工作人员、高校研究人员，探究”小小蓝精灵，铺就致富路“背后的秘密，亲身体会乡村振兴的生机活力。",
						],
				// pageIndex: 1,
				// loadding: false,
				// pullUpOn: true,
				// opacity: 1
			};
		},
		methods: {
			onclick: function(idx){
				uni.navigateTo({
					url: '/pages/component/detail/detail'
				});
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
		text-align: center;
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
		top: 15px;
		width: 100%;
		height: 57px;
		color: rgba(251, 251, 251, 1);
		font-size: 20px;
		text-align: center;
		font-family: PingFangSC-regular;
	}
	
	.text4{
		position: absolute;
		left: 25%;
		top: 45px;
		width: 85px;
		height: 41px;
		color: rgba(251, 251, 251, 1);
		font-size: 14px;
		text-align: left;
		font-family: PingFangSC-regular;
	}
	
	.text5{
		position: absolute;
		top: 15px;
		width: 100%;
		height: 57px;
		color: rgba(251, 251, 251, 1);
		font-size: 20px;
		text-align: center;
		font-family: PingFangSC-regular;
	}
	
	.product-box1{
		position: absolute;
		left: 16px;
		top: 325px;
		width: 166px;
		height: 101px;
		line-height: 20px;
		border-radius: 10px;
		background-color: rgba(105, 192, 255, 1);
		text-align: center;
		box-shadow: 0px 2px 6px 0px rgba(145, 213, 255, 1);
	}
	
	.product-box2{
		position: absolute;
		left: 195px;
		top: 326px;
		width: 166px;
		height: 101px;
		line-height: 20px;
		border-radius: 10px;
		background-color: rgba(149, 222, 100, 1);
		text-align: center;
		box-shadow: 0px 2px 6px 0px rgba(217, 247, 190, 1);
	}
	
	.show-text{
		position: absolute;
		left: 137px;
		top: 442px;
		width: 102px;
		height: 34px;
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
		left: 18px;
		top: 490px;
		width: 343px;
		height: 248px;
		line-height: 20px;
		border-radius: 5px;
		background-color: rgba(255, 255, 255, 1);
		text-align: center;
		border: 1px solid rgba(221, 219, 219, 1);
	}
	
	.stats2{
		position: absolute;
		left: 18px;
		top: 752px;
		width: 343px;
		height: 248px;
		line-height: 20px;
		border-radius: 5px;
		background-color: rgba(255, 255, 255, 1);
		text-align: center;
		border: 1px solid rgba(221, 219, 219, 1);
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
</style>
