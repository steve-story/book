<template>
	<view class="container">
		
		<view class="intro">本项目已包含uni ui组件，无需import和注册，可直接使用。在代码区键入字母u，即可通过代码助手列出所有可用组件。光标置于组件名称处按F1，即可查看组件文档。</view>
		<text class="intro">详见：</text>
		<uni-link :href="href" :text="href"></uni-link>
		
		<view class="cate-lv2" v-for="(item2, i2) in cateLevel2" :key="i2">
			<!-- 二级分类标题 -->
			<view class="cate-lv2-title">/ {{item2.cat_name}} /</view>
			<!-- 三级分类列表 -->
			<view class="cate-lv3-list">
				<view class="cate-lv3-item" v-for="(item3, i3) in item2.children" :key="i3" >
					<!-- @click="gotoCourseList(item3)" -->
					<image :src="item3.cat_icon"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				href: 'https://uniapp.dcloud.io/component/README?id=uniui'
			}
		},
		methods: {

		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
