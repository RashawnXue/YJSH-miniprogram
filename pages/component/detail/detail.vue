<template>
	<view class="container">
		<view class="title">
			<text> {{title}} </text>
		</view>
		
		<view class="time">
			<text> {{time}} </text>
		</view>
		
		<view class="content1">
			<text> &emsp;&emsp;{{content1}} </text>
		</view>
		
		<view class="pic">
			<image src="../../../static/blueberry/成果展示1.png"></image>
		</view>
		
		<view class="content2">
			<text> &emsp;&emsp;{{content2}} </text>
		</view>
		
		<view class="prev-box">
			<button disabled class="prev-button" @click="Prev()"> 上一篇 </button>
			<text class="prev-text"> 已经是第一篇 </text>
		</view>
		
		<view class="next-box">
			<button class="next-button" @click="Next()"> 下一篇 </button>
			<text class="next-text"> 行业内专家评河南蓝莓种植成果 </text>
		</view>
	</view>
</template>

<script>
	// #ifdef APP-PLUS
	const dom = weex.requireModule('dom');
	// #endif
	
	export default {
		data() {
			return {
				idx: 1,
				max_idx: 2,
				title:"蓝莓种植园区发展成果",
				time:"2023年7月22日",
				content1:"      2012年，经农业部蓝莓树莓项目首席专家李亚东教授考察，认为库区乡自然环境良好，适于蓝莓种植，遂有河南河洛农林科技公司在东许庄村引种成功。",
				content2:"      经过10年发展，库区乡先后吸引豫尧、蓝沃、奕源、沃德等众多实力雄厚的专业公司落地生根。目前，全乡共发展蓝莓种植园区19个，种植面积6800余亩，其中17个种植园区在东许庄村，辐射婆娑、栗村、搬走岭、火石呀等行政村。主要种植品种有蓝风、奥尼尔、米斯提、雷哥西等，亩产高达2000斤，当前处于盛果期蓝莓3000余亩，年产值超过1亿元。培养了以蓝莓种植大户党宪坤、王建有、刘伟、王建超、王国朝等为主力军的“土专家”、“田秀才”，“头雁”作用发挥明显，带领群众通过蓝莓产业过上幸福生活。"
			}
		},
		onReady() {
			this.pageHeight = uni.getSystemInfoSync().windowHeight;
			console.log(this.idx);
			// uni.createSelectorQuery().in(this).select('#head').boundingClientRect().exec(rect => {
			// 	this.$refs.sublist.setSpecialEffects({
			// 		id: this.parentListId,
			// 		headerHeight: rect[0].height
			// 	});
			// });
		},
		methods: {
			onrefresh(e) {
				this.refreshing = true;
				this.refreshText = "刷新中...";
				setTimeout(() => {
					this.refreshing = false;
					this.refreshFlag = false;
					this.refreshText = "已刷新";
				}, 2000)
			},
			onpullingdown(e) {
				if (this.refreshing) {
					return;
				}
	
				this.pulling = false;
				if (Math.abs(e.pullingDistance) > Math.abs(e.viewHeight)) {
					this.refreshFlag = true;
					this.refreshText = "释放立即刷新";
				} else {
					this.refreshFlag = false;
					this.refreshText = "下拉可以刷新";
				}
			},
			
			Prev(){
				console.log("prev");
			}
			
			Next(){
				console.log("next");
			}
		}
	}
</script>

<style>
	.title{
		margin-top: 20px;
		margin-bottom: 10px;
		width: 100%;
		height: 25px;
		color: rgba(16, 16, 16, 1);
		font-size: 18px;
		text-align: center;
		font-family: PingFangSC-regular;
	}
	
	.time{
		margin-bottom: 10px;
		width: 100%;
		height: 25px;
		color: rgba(108, 108, 108, 1);
		font-size: 14px;
		text-align: center;
		font-family: PingFangSC-regular;
	}
	
	.content1{
		margin-left: 5%;
		margin-bottom: 10px;
		width: 90%;
		color: rgba(16, 16, 16, 1);
		font-size: 14px;
		text-align: left;
		font-family: PingFangSC-regular;
	}
	
	.content2{
		margin-left: 5%;
		margin-bottom: 10px;
		width: 90%;
		color: rgba(16, 16, 16, 1);
		font-size: 14px;
		text-align: left;
		font-family: PingFangSC-regular;
	}
	
	.pic{
		margin-left: 5%;
		margin-bottom: 10px;
		width: 90%;
	}
	
	.container{
		flex: 1;
		flex-direction: column;
	}
	
	.prev-box{
		margin-left: 5%;
		margin-bottom: 10px;
		width: 90%;
		height: 30px;
		flex-direction: row;
	}
	
	.prev-button{
		position: absolute;
		width: 80px;
		height: 35px;
		margin-left: 0%;
		border-radius: 4px;
		background-color: rgba(190, 190, 190, 1);
		color: rgba(255, 255, 255, 1);
		font-size: 14px;
		text-align: center;
		font-family: Microsoft Yahei;
	}
	
	.prev-text{
		position: absolute;
		margin-top: 8px;
		margin-left: 25%;
		width: 75%;
		height: 20px;
		color: rgba(154, 154, 154, 1);
		font-size: 14px;
		text-align: left;
		font-family: PingFangSC-regular;
	}
	
	.next-box{
		margin-left: 5%;
		margin-bottom: 10px;
		width: 90%;
		height: 30px;
		flex-direction: row;
	}
	
	.next-button{
		position: absolute;
		width: 80px;
		height: 35px;
		margin-left: 0%;
		border-radius: 4px;
		background-color: rgba(255, 255, 255, 1);
		color: rgba(16, 16, 16, 1);
		font-size: 14px;
		text-align: center;
		font-family: Microsoft Yahei;
		border: 1px solid rgba(187, 187, 187, 1);
	}
	
	.next-text{
		position: absolute;
		margin-top: 8px;
		margin-left: 25%;
		width: 75%;
		height: 20px;
		color: rgba(16, 16, 16, 1);
		font-size: 14px;
		text-align: left;
		font-family: PingFangSC-regular;
	}
</style>