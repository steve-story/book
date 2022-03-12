<template>
	<view style="background-color: #FAFAFA;">
		<view class="search_box">
			<uni-search-bar @input="input" :radius="100" cancelButton="none"></uni-search-bar>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				timer: null,
				keyword: ''
			};
		},
		methods: {
			input(e) {
				// 清除 timer 对应的延时器
				clearTimeout(this.timer)
				// 如果 500 毫秒内，没有触发新的输入事件，则为搜索关键词赋值
				this.timer = setTimeout(() => {
					this.keyword = e
					console.log(e) // e=value 是最新的搜索内容
				}, 500)
			}
		}
	}
</script>

<style lang="scss">
	.search_box {
		//吸顶效果
		position: sticky;
		top: 0;
		z-index: 999;
	}
</style>
