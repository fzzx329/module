 <!-- 取消过渡时间改变ul的位置 无回滚轮播图 -->
<template>
	<div id="lbt" v-bind:style="{width:width+'px',height:height+'px'}" v-on:mouseover="stop()" v-on:mouseout="autoPlay()">
			<ul class="tpk" v-bind:style="{width:W,height:height+'px',left:-width+'px',transform:d,transition:jsj}" v-on:transitionend="cz">
				<li>
					<a href="">
						<img v-bind:src="tp[tp.length-1]" v-bind:style="{width:width+'px',height:height+'px'}">
					</a>
				</li>
				<li v-for="(img,index) in tp" :key="index">
					<a href="#">
						<img v-bind:src="img" v-bind:style="{width:width+'px',height:height+'px'}">
					</a>
				</li>
				<li>
					<a href="">
						<img v-bind:src="tp[0]" v-bind:style="{width:width+'px',height:height+'px'}">
					</a>
				</li>
			</ul>
		<ul class="xdk">
			<li v-for="(img,index) in tp" :key="index" v-on:click="xzPlay(index)" v-bind:class="{'up':index===xdcs}"></li>
		</ul>
		<div class="left" v-on:click="ys && leftPlay()">《</div>
		<div class="right" v-on:click="ys && rightPlay()">》</div>	<!-- ys为true时才可执行点击事件 -->	
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
				play:null,
				gdsj:"all 0.5s",
				jsj:"none",
				d:"",
				xdcs:0,
				ys:true
			}
		},
		computed:{
			W(){
				return (this.tp.length+2)*this.width+"px";
			},/*获取总长度*/
		},
		watch:{
			cs:function(val){
				this.d='translateX('+(-val*this.width)+'px)';
				
				if(val*this.width==this.width*this.tp.length){
					this.xdcs=0;
				}else if(-val*this.width==this.width){
					this.xdcs=this.tp.length-1;
				}else{
					this.xdcs=val;
				}
			}
		},
		methods:{
			rightPlay(){
				this.jsj=this.gdsj;
				if(this.cs===this.tp.length){
					this.cs=0;
				}
				this.cs++;
				this.ys=false;
			},
			leftPlay(){
				this.jsj=this.gdsj;
				if(this.cs==-1){
					this.cs=this.tp.length-1;
				}
				this.cs--;
				this.ys=false;
			},
			xzPlay(c){
				this.jsj=this.gdsj;
				this.cs=c;
				this.xdcs=c
			},
			autoPlay(){
				this.play=setInterval(this.rightPlay,3000);
			},
			stop(){
				clearInterval(this.play);
			},
			cz(){
				console.log(this.cs*this.tp.length);
				this.ys=true;
				if(this.cs*this.width==this.width*this.tp.length){
					this.jsj="none";
					this.d='translateX('+0+'px)';
					this.cs=0;
				}else if(-this.cs*this.width==this.width){
						this.jsj="none";
						this.d='translateX('+(-this.width*(this.tp.length-1))+'px)';
						this.cs=this.tp.length-1;
				}
			}
		},
		created(){
			this.autoPlay();
		}
	}
</script>