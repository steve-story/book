<template>
	<view class="my-search-container" :style="{'background-color': bgcolor}">
		<!-- 使用 view 组件模拟 input 输入框的样式 -->
		<view class="my-search-box" :style="{'border-radius': radius + 'px'}"  @click="searchBoxHandler">
			<uni-icons type="search" size="17"></uni-icons>
			<text class="placeholder">搜索</text>
		</view>
	</view>
</template>

<script>
	export default {
		//可自定义搜索组件的背景颜色和圆角尺寸。
		props: {
			// 背景颜色
			bgcolor: {
				type: String,
				default: '#C00000'
			},
			// 圆角尺寸
			radius: {
				type: Number,
				// 单位是 px
				default: 18
			}
		},
		name: "my-search",
		data() {
			return {

			};
		},
		methods: {
			searchBoxHandler() {
				// 触发外界通过 @click 绑定的 click 事件处理函数
				this.$emit('click')
			}
		}
	}
</script>

<style lang="scss">
	.my-search-container {
		background-color: #c00000;
		height: 50px;
		padding: 0 10px;
		display: flex;
		align-items: center; //纵轴居中
	}

	.my-search-box {
		height: 36px;
		background-color: #ffffff;
		border-radius: 15px;
		width: 100%;
		display: flex;
		//flex-direction: column;//浮动方向，确定主轴
		align-items: center; //副轴（纵轴）居中
		justify-content: center; //主轴（横轴）居中

		.placeholder {
			font-size: 15px;
			margin-left: 5px;
		}
	}
</style>
