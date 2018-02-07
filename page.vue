<template>
	<div class="page-bar" v-cloak>
		<ul>
			<!--上一页分页按钮-->
			<li v-if="cur>1">
				<a @click="cur--,pageClick()">上一页</a>
			</li>
			<li v-if="cur==1">
				<a class="banclick">上一页</a>
			</li>
			<!--显示的当前页吗数-->
			<li v-for="index in indexs" :class="{'active': cur == index}">
				<a @click="btnClick(index)">{{ index }}</a>
			</li>
			<!--下一页分页按钮-->
			<li v-if="cur!=all">
				<a @click="cur++,pageClick()">下一页</a>
			</li>
			<li v-if="cur == all">
				<a class="banclick">下一页</a>
			</li>
			<!--总页数标签-->
			<li>
				<a>共<i>{{all}}</i>页</a>
			</li>
		</ul>
	</div>
</template>

<script>
	export default {
	
		data() {
			return {
				all:20, //总页数
				cur:1, //当前页码
			}
		},
		computed: {
			indexs() {
				var left = 1;
				var right = this.all;
				var arr = [];
				if(this.all >= 5) {
					if(this.cur > 3 && this.cur < this.all - 2) {
						left = this.cur - 2
						right = this.cur + 2
					} else {
						if(this.cur <= 3) {
							left = 1
							right = 5
						} else {
							right = this.all
							left = this.all - 4
						}
					}
				}
				//while循环
				while(left <= right) {
					arr.push(left)
					left++
				}
				return arr
			}

		},
		methods: {
			btnClick(data) { //页码点击事件
				if(data != this.cur) {
					this.cur = data
				}
			},
			pageClick() {
				console.log('现在在' + this.cur + '页');
			}
		},
		watch: {
			cur() {
				console.log(this.cur);
			}
		}

	}
</script>

<style scoped>
	[v-cloak] {
		display: none;
	}
	.page-bar{
		width:500px;
		margin:10px auto;
		overflow: hidden;
	}
	
	ul,
	li {
		margin: 0px;
		padding: 0px;
	}
	
	li {
		list-style: none
	}
	
	.page-bar li:first-child>a {
		margin-left: 0px
	}
	
	.page-bar a {
		border: 1px solid #ddd;
		text-decoration: none;
		position: relative;
		float: left;
		padding: 6px 12px;
		margin-left: -1px;
		line-height: 1.42857143;
		color: #337ab7;
		cursor: pointer
	}
	
	.page-bar a:hover {
		background-color: #eee;
	}
	
	.page-bar a.banclick {
		cursor: not-allowed;
	}
	
	.page-bar .active a {
		color: #fff;
		cursor: default;
		background-color: #337ab7;
		border-color: #337ab7;
	}
	
	.page-bar i {
		font-style: normal;
		color: #d44950;
		margin: 0px 4px;
		font-size: 12px;
	}
</style>