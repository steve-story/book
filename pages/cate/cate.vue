<template>
	<view>
		<my-search @click="gotoSearch()"></my-search>

		<view class="scroll-view-container">
			<!-- 左侧的滚动视图区域 -->
			<scroll-view class="left-scroll-view" scroll-y :style="{height: wh + 'px'}">
				<block v-for="(item, i) in cateList" :key="i">
					<view :class="['left-scroll-view-item', i === active ? 'active' : '']" @click="activeChanged(i)">
						{{item.cat_name}}
					</view>
				</block>
			</scroll-view>
			<!-- 右侧的滚动视图区域 -->
			<scroll-view class="right-scroll-view" scroll-y :style="{height: wh + 'px'}" :scroll-top="scrollTop">
				<!-- 三级分类列表 -->
				<view class="cate-lv2-list">
					<view class="cate-lv2-item" v-for="(item2, i2) in cateLevel2" :key="i2"
						@click="gotoCourseList(item2)">

						<image :src="item2.cat_icon"></image>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 窗口的可用高度windowheight
				wh: 0,
				active: 0,
				scrollTop: 0,
				cateList: [{
					cat_id: '1',
					cat_name: '通识必修',
					children: [{
						course_id: '1',
						course_name: '大学英语精读',
						cat_icon: '/static/cate_icons/course1.png',
					}, {
						course_id: '2',
						course_name: '高等数学',
						cat_icon: '/static/cate_icons/course2.png',
					}, {
						course_id: '3',
						course_name: '中国近代史纲要',
						cat_icon: '/static/cate_icons/course3.png',
					}]
				}, {
					cat_id: '2',
					cat_name: '通识选修',
					children: [{
						course_id: '4',
						course_name: '中日茶道文化',
						cat_icon: '/static/cate_icons/course4.png',
					}, {
						course_id: '5',
						course_name: '考古与人类',
						cat_icon: '/static/cate_icons/course5.png',
					}, {
						course_id: '6',
						course_name: '幸福心理学',
						cat_icon: '/static/cate_icons/course6.png',
					}, {
						course_id: '7',
						course_name: '中国古代史',
						cat_icon: '/static/cate_icons/course7.png',
					}, {
						course_id: '8',
						course_name: '国际关系与中国外交',
						cat_icon: '/static/cate_icons/course8.png',
					}]
				}, {
					cat_id: '2',
					cat_name: '计算机类',
					children: [{
						course_id: '9',
						course_name: '数据库系统原理',
						cat_icon: '/static/cate_icons/course9.png',
					}, {
						course_id: '10',
						course_name: '计算机组成原理',
						cat_icon: '/static/cate_icons/course10.png',
					}, {
						course_id: '11',
						course_name: '操作系统',
						cat_icon: '/static/cate_icons/course11.png',
					}, {
						course_id: '12',
						course_name: '大学计算机基础',
						cat_icon: '/static/cate_icons/course12.png',
					}]
				}],
				cateLevel2: [],
			};
		},
		onLoad() {
			// 获取当前系统的信息
			const sysInfo = uni.getSystemInfoSync()
			// 为 wh 窗口可用高度动态赋值
			this.wh = sysInfo.windowHeight - 50 //搜索区50px
			this.cateLevel2 = this.cateList[0].children
			// this.getCateList();
		},
		methods: {
			// async getCateList() {
			// 	const {
			// 		data: res
			// 	} = await uni.$http.get('https://api-hmugo-web.itheima.net/api/public/v1/categories')
			// 	if (res.meta.status !== 200) return uni.$showMsg()

			// 	this.cateList = res.message
			// 	console.log(res.message)
			// 	// 为二级分类赋值
			// 	this.cateLevel2 = res.message[0].children
			// },
			activeChanged(i) {
				this.active = i
				// 为二级分类列表重新赋值
				this.cateLevel2 = this.cateList[i].children
				//：动态绑定必须在scrollTop变化才变化
				this.scrollTop = this.scrollTop === 0 ? 1 : 0
			},
			gotoCourseList(item2) {
				uni.navigateTo({
					url: '/subpkg/course_list/course_list?course_id=' + item2.course_id
				})
			},
			gotoSearch() {
				uni.navigateTo({
					url: '/subpkg/search/search',
				})
			}
		}
	}
</script>

<style lang="scss">
	.scroll-view-container {
		display: flex;

		.left-scroll-view {
			width: 118px;

			.left-scroll-view-item {
				line-height: 60px; //相比于height文字会居中
				background-color: #f7f7f7; //背景灰色
				text-align: center;
				font-size: 15px;

				// 激活项的样式
				&.active {
					background-color: #ffffff;
					position: relative;

					// 渲染激活项左侧的红色指示边线
					&::before {
						content: ' ';
						display: block;
						width: 3px;
						height: 30px;
						background-color: #c00000;
						position: absolute;
						left: 0;
						top: 50%;
						transform: translateY(-50%);
					}
				}
			}
		}

		// .cate-lv2-title {
		// 	font-size: 14px;
		// 	font-weight: bold;
		// 	text-align: center;
		// 	padding: 15px 0;
		// }

		.cate-lv2-list {
			display: flex;
			flex-wrap: wrap;

			.cate-lv2-item {
				width: 49%;
				margin-bottom: 10px;
				display: flex;
				flex-direction: column;
				align-items: center;

				image {
					width: 280rpx;
					height: 265rpx;
				}

				text {
					font-size: 12px;
				}
			}
		}
	}
</style>
