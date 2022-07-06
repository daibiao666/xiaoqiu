<template>
	<view class="content">
		<!-- 已选中列表 -->
		<view class="list-box">
			<view 
			v-for="(item,index) in selectList"
			:key="index"
			class="list-box_item" 
			:style="{backgroundColor: item.color}">{{item.text}}</view>
		</view>
		<block
		v-if="list.length > 0"
		>
			<view
			v-for="(item,index) in list"
			:key="item"
			ref="box"
			:id="'box'+index"
			@tap="onSelect(index,getColor(index))"
			class="box"
			:style="{
				backgroundColor: getColor(index),
				top: item.style.top,
				left: item.style.left,
			}"
			:class="item.class"
			>{{item.text}}</view>
		</block>
	</view>
</template>

<script>
	const color0 = ['#ffbe0b','#fb5607','#ff006e','#3a86ff','#8338ec','#8ac926','#fcf6bd','#00bbf9','#ff7d00','#ffcad4']
	const color1 = ['#ddfff7','#80b918','#17c3b2','#d68c45','#ffd500','#c1121f','#a9def9','#e4c1f9','#7bf1a8','#80ed99']
	const color2 = ['#f8961e','#fff3b0','#e36414','#e0fbfc','#b9fbc0','#0466c8','#ffe169','#9381ff','#e7e6f7','#f3de8a']
	const demo = [
		[
			{
				text: 'IT'
			},
			{
				text: '前端'
			},
			{
				text: '后端'
			}
		],
		[
			{
				text: 'java'
			},
			{
				text: 'c++'
			},
			{
				text: 'python'
			}
		],
		[
			{
				text: 'vue'
			},
			{
				text: 'react'
			},
			{
				text: 'webpack'
			}
		],
		[
			{
				text: 'uni-app'
			},
			{
				text: 'flutter'
			},
			{
				text: 'web3.0'
			}
		]
	]
	export default {
		computed: {
			getColor: function() {
				let index = Math.floor(Math.random() * color0.length)
				return (type) => {
					switch(type) {
						case 0: return color0[index]
						case 1: return color1[index]
						case 2: return color2[index]
					}
				}
			}
		},
		data() {
			return {
				x: 0,
				y: 0,
				windowHeight: 0, // 屏幕高度
				windowWidth: 0, // 屏幕宽度
				currentClass: 'step',
				list: [],
				selectList: [],
				currentIndex: null,
				isClick: false // 是否允许被点击
			}
		},
		onLoad() {
			this.init(demo[0])
		},
		methods: {
			init(list) {
				this.isClick = false
				setTimeout(() => {
					this.isClick = true
				},6000)
				this.list = list
				// 数据处理
				for (let i = 0; i < this.list.length; i++) {
					let calssStr = 'step'+ i
					this.list[i].class = calssStr
					this.list[i].style = {}
				}
			},
			// 选择
			onSelect(index,color) {
				if(!this.isClick) return
				for (let i = 0; i < this.list.length; i++) {
					if(index === i) {
						this.$set(this.list[i],'class','fixed' + index)
					}else {
						this.$set(this.list[i],'class','hide')
					}
				}
				let item = this.list[index]
				item.color = color
				setTimeout(() => {
					const paddingTop = this.selectList.length > 0 ?  this.selectList.length*30 + 50 : 50
					const top = this.selectList.length*150 + paddingTop
					this.list[index].style = {
						top: `${top}rpx`,
						left: '50rpx'
					}
					this.$forceUpdate()
				},0)
				setTimeout(() => {
					this.selectList.push(item)
					this.list = []
					if(this.selectList.length > 3) return
					this.init(demo[this.selectList.length])
				},1500)
				this.$forceUpdate()
			}
		}
	}
</script>

<style lang="scss" scoped>
.list-box {
	padding-left: 30rpx;
	padding-top: 30rpx;
	box-sizing: border-box;
	&_item {
		width: 150rpx;
		height: 150rpx;
		text-align: center;
		line-height: 150rpx;
		border-radius: 50%;
		margin-bottom: 30rpx;
	}
}
.box {
	width: 100rpx;
	height: 100rpx;
	text-align: center;
	line-height: 100rpx;
	background-color: skyblue;
	border-radius: 50%;
	position: fixed;
	font-size: 28rpx;
	color: #333333;
}
.step0 {
	animation-name: step0-animate;
	animation-duration: 6s;
	animation-timing-function: ease-in-out;
	animation-fill-mode: forwards;
}
@keyframes step0-animate {
	0% {
		left: 300rpx;
		bottom: 0;
	}
	25% {
		left: 100rpx;
		bottom: 150rpx;
	}
	50% {
		left: 300rpx;
		bottom: 250rpx;
	}
	75% {
		left: 100rpx;
		bottom: 400rpx;
		transform: scale(1.2);
	}
	100% {
		left: 450rpx;
		bottom: 600rpx;
		transform: scale(1.5);
	}
}


.step1 {
	animation-name: step1-animate;
	animation-duration: 6s;
	animation-timing-function: ease-in-out;
	animation-fill-mode: forwards;
}
@keyframes step1-animate {
	0% {
		left: 400rpx;
		bottom: 0;
	}
	25% {
		left: 450rpx;
		bottom: 200rpx;
	}
	50% {
		left: 100rpx;
		bottom: 400rpx;
	}
	75% {
		left: 200rpx;
		bottom: 500rpx;
		transform: scale(1.2);
	}
	100% {
		left: 600rpx;
		bottom: 700rpx;
		transform: scale(1.5);
	}
}

.step2 {
	animation-name: step2-animate;
	animation-duration: 7s;
	animation-timing-function: ease-in-out;
	animation-fill-mode: forwards;
}
@keyframes step2-animate {
	0% {
		left: 350rpx;
		bottom: 0;
	}
	30% {
		left: 550rpx;
		bottom: 200rpx;
	}
	30% {
		left: 550rpx;
		bottom: 300rpx;
	}
	75% {
		left: 600rpx;
		bottom: 400rpx;
	}
	100% {
		left: 50rpx;
		bottom: 800rpx;
		transform: scale(1.5);
	}
}



.hide {
	display: none;
}
.fixed0 {
	transform: scale(1.5);
	position: fixed;
	top: calc(100vh - 600rpx - 75rpx);
	left: 450rpx;
	transition: all 1.5s; 
}
.fixed1 {
	transform: scale(1.5);
	position: fixed;
	top: calc(100vh - 700rpx - 75rpx);
	left: 600rpx;
	transition: all 1.5s; 
}
.fixed2 {
	transform: scale(1.5);
	position: fixed;
	top: calc(100vh - 800rpx - 75rpx);
	left: 50rpx;
	transition: all 1.5s; 
}
</style>
