 <!-- 回滚移动过渡轮播图 -->
<template>
	<div id="lbt" v-bind:style="{width:width+'px',height:height+'px'}" v-on:mouseover="stop()" v-on:mouseout="autoPlay()">
			<ul class="tpk" v-bind:style="{width:W,height:height+'px',transform:yd,transition:gdsj}">
				<li v-for="(img,index) in tp" :key="index">
					<a href="#">
						<img v-bind:src="img" v-bind:style="{width:width+'px',height:height+'px'}">
					</a>
				</li>
			</ul>
		<ul class="xdk">
			<li v-for="(img,index) in tp" :key="index" v-on:click="xzPlay(index)" v-bind:class="{'up':index===cs}"></li>
		</ul>
		<div class="left" v-on:click="leftPlay">《</div>
		<div class="right" v-on:click="rightPlay">》</div>		
	</div>
</template>
<style type="text/css">
	#lbt{
		margin:0 auto;
		position: relative;
		overflow: hidden;
	}/*外面大框*/
	#lbt ul{
		margin: 0;
		list-style: none;
		overflow: hidden;
	}/*初始化ul*/
	.tpk{
		position: absolute;
		left: 0;
		top: 0;
	}
	.tpk li{
		float: left;
	}
	.tpk img{
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
		computed:{
			W(){
				return (this.tp.length)*this.width+"px";
			},/*获取总长度*/
			yd(){
				return 'translateX('+(-this.cs*this.width)+'px)';
			},/*移动距离*/
			gdsj(){
				return "all 0.5s";
			}/*移动时间*/
		},
		methods:{
			rightPlay(){
				this.cs++;
				if(this.cs===this.tp.length){
					this.cs=0;
				}
			},
			leftPlay(){
				if(this.cs==0){
					this.cs=this.tp.length;
				}
				this.cs--;
			},
			xzPlay(c){
				this.cs=c;
			},
			autoPlay(){
				this.play=setInterval(this.rightPlay,3000);
			},
			stop(){
				clearInterval(this.play);
			},
		},
		created(){
			this.autoPlay();
		}
	}
</script>