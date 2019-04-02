 <!-- vue渐变轮播图组件 -->
<template>
	<div id="lbt" v-bind:style="{width:width+'px',height:height+'px'}" v-on:mouseover="stop()" v-on:mouseout="autoPlay()"><!-- 鼠标进出 -->
		<transition-group name="dh">
					<a class="tpa" href="#" v-for="(img,index) in tp" :key="index" v-show="index==cs">
						<img v-bind:src="img" v-bind:style="{width:width+'px',height:height+'px'}">
					</a>
		</transition-group><!-- 过度动画 -->
		<ul class="xdk">
			<li v-for="(img,index) in tp" :key="index" v-on:click="xzPlay(index)" v-bind:class="{'up':index===cs}"></li>
		</ul><!-- 小点列 -->
		<div class="left" v-on:click="leftPlay">《</div>
		<div class="right" v-on:click="rightPlay">》</div>		
	</div>
</template>
<style type="text/css">
	#lbt{
		position: relative;
		overflow: hidden;
	}/*外面大框*/
	#lbt ul{
		margin: 0;
		list-style: none;
		overflow: hidden;
	}/*初始化ul*/
	.tpa{
		position: absolute;
		left: 0;
		top: 0;
	}/*img的a外框*/
	.tpa img{
		vertical-align: top;
	}
	.xdk{
		padding: 5px;
		position: absolute;
		left: 50%;
		bottom: 10px;
		transform: translateX(-50%);
	}/*小点ul 自动水平居中*/
	.xdk li{
		margin: 0 6px;
		float: left;
		height: 10px;
		width: 10px;
		border: 2px solid #fff;
		border-radius: 50%;
		background-color: #fff;
		cursor:pointer;	
	}/*小点*/
	.xdk li:hover{
		background-color: #999;
	}/*小点hover效果*/
	.up{
		background-color: #888 !important;
		border-color: #888 !important;
	}/*小点变色*/
	.left,.right{
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		font-size: 20px;
		text-align: center;
		line-height: 40px;
		width: 24px;
		height: 40px;
		border-radius: 4px;
		background-color: rgba(0,0,0,0.3);
		color: #777;
		cursor:pointer;	
	}/*左右*/
	.left{left: 10px;}
	.right{right: 10px;}
	.left:hover{color: #fff}
	.right:hover{color: #fff}
	/*-------------以下为vue过度属性--------------*/
	.dh-enter-active, .dh-leave-active {
		transition: opacity 1s;
	}
	.dh-enter, .dh-leave-to{
		opacity: 0;
	}
	/*-------------以上为vue过度属性--------------*/
</style>
<script type="text/javascript">
	export default{
		name:"lbt",
		data(){
			return{
				tp:[
					'https://www.yangqq.com/skin/blankgd/images/banner01.jpg',
		          	'https://www.yangqq.com/skin/blankgd/images/banner02.jpg',
		          	'https://www.yangqq.com/skin/blankgd/images/banner03.jpg',
				],
				width:800,
				height:300,
				cs:0,
				play:null
			}
		},
		methods:{
			rightPlay(){
				this.cs++;
				if(this.cs===this.tp.length){
					this.cs=0;
				}
			},/*下一张*/
			leftPlay(){
				if(this.cs==0){
					this.cs=this.tp.length;
				}
				this.cs--;
			},/*上一张*/
			xzPlay(c){
				this.cs=c;
			},/*小点选择*/
			autoPlay(){
				this.play=setInterval(this.rightPlay,3000);
			},/*自动播放定时器*/
			stop(){
				clearInterval(this.play);
			}/*停止自动播放*/
		},
		created(){
			this.autoPlay();
		}/*初始化自动播放*/
	}
</script>