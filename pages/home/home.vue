<template>
	<view>
		<!-- 轮播图区 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
			<!-- 循环渲染轮播图的 item 项 -->
			<swiper-item v-for="(item, i) in swiperList" :key="i">
				<navigator class="swiper-item" :url="'/subpkg/ad_detail/ad_detail?ad_id='+item.ad_id">
					<!-- 动态绑定图片的 src 属性 -->
					<image :src="item.image_src"></image>
				</navigator>
			</swiper-item>
		</swiper>

		<!-- 分类导航区域 -->
		<!-- 		<view class="nav-list">
			<view class="nav-item" v-for="(item, i) in navList" :key="i" @click="navClickHandle(item)">
				<image :src="item.image_src" class="nav-img"></image>
			</view>
		</view> -->

		<!-- 新闻栏 -->
		<view class="news_line">
			<image src='/static/home_icons/news.png' class="news_img"></image>
			<view class="news_word">
				新闻信息
			</view>
			<view class="more" @click="newsClickHandle()">
				<image src="/static/home_icons/more.png" class="more_img"></image>
			</view>
		</view>
		<!-- 新闻推荐区 -->
		<view class="news_list">
			<view class="news_item" v-for="(item,i) in newsList" :key="i" @click="newsListClickHandle()">
				<image :src="item.image_src" class="newsList_img"></image>
			</view>
		</view>
		
		<!-- 课程信息 -->
		<view class="course_line">
			<image src='/static/home_icons/courseicon.png' class="course_img"></image>
			<view class="course_word">
				课程推荐
			</view>
			<view class="more" @click="courseClickHandle()">
				<image src="/static/home_icons/more.png" class="more_img"></image>
			</view>
		</view>
		<!-- 新闻推荐区 -->
		<view class="course_list">
			<view class="course_item" v-for="(item,i) in courseList" :key="i" @click="courseListClickHandle(item)">
				<image :src="item.image_src" class="courseList_img"></image>
			</view>
		</view>
		


	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 轮播图的数据列表
				swiperList: [{
					image_src: '/static/home_icons/ad1.jpg',
					ad_id: '1'
				}, {
					image_src: '/static/home_icons/ad2.jpg',
					ad_id: '2'
				}, {
					image_src: '/static/home_icons/ad3.jpg',
					ad_id: '3'
				}],
				navList: [],
				newsList: [{
					image_src: '/static/home_icons/news1.png',
					news_id: '1'
				}, {
					image_src: '/static/home_icons/news2.png',
					news_id: '2'
				}, {
					image_src: '/static/home_icons/news3.png',
					news_id: '3'
				}],
				courseList:[{
					image_src: '/static/home_icons/course1.png',
					courses_id: '1'
				},{
					image_src: '/static/home_icons/course2.png',
					courses_id: '2'
				}]
			};
		},
		onLoad() {
			// 在小程序页面刚加载的时候，调用获取轮播图数据的方法
			// this.getSwiperList()
			// this.getNavList()
			// this.getFloorList()
		},
		methods: {
			// async getSwiperList() {
			// 	//发起请求
			// 	const {data: res} = await uni.$http.get('https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata')
			// 	if (res.meta.status !== 200) return uni.$showMsg()
			// 	console.log(res);
			// 	//成功，为 data 中的数据赋值
			// 	this.swiperList = res.message
			// 	uni.$showMsg('数据请求成功')
			// },
			// async getNavList() {
			// 	const {
			// 		data: res
			// 	} = await uni.$http.get('https://api-hmugo-web.itheima.net/api/public/v1/home/catitems')
			// 	if (res.meta.status !== 200) return uni.$showMsg()

			// 	this.navList = res.message
			// 	console.log(res);
			// },
			newsClickHandle() {
				uni.switchTab({
					url: '/pages/new/new'
				})
			},
			courseClickHandle() {
				uni.switchTab({
					url: '/pages/cate/cate'
				})
			}
		}
	}
</script>

<style lang="scss">
	swiper {
		height: 350rpx;

		.swiper-item,
		image {
			width: 100%;
			height: 100%;
		}
	}
	// .nav-list {
	// 	display: flex;
	// 	justify-content: space-around;
	// 	margin: 15px 0px; //上下 左右外边距

	// 	.nav-img {
	// 		width: 128rpx;
	// 		height: 140rpx;
	// 	}
	// }
	.news_line {
		height: 85rpx;
		display: flex;
		flex-direction: row;
		// border-bottom:  solid #646566;
		background-color: #FFFFFF;

		.news_img {
			margin: 12rpx;
			margin-left: 12rpx;
			width: 60rpx;
			height: 60rpx;
		}

		.news_word {
			margin-top: 16rpx;
		}
	}
	.more {
		margin-left: auto;
		margin-top: 12rpx;
	
		// display: flex;
		// flex-direction: row;
		// justify-content: flex-end;
		.more_img {
			margin-right: 14rpx;
			width: 60rpx;
			height: 60rpx;
		}
	}
	.course_list,.news_list {
		display: flex;
		justify-content: space-around;
		margin-top: 10rpx;
		margin-bottom: 10rpx;
	}
	.newsList_img {
		width: 230rpx;
		height: 260rpx;
	}
	.courseList_img{
		width: 308rpx;
		height: 280rpx;
	}
	
	.course_line{  
		height: 85rpx;
		display: flex;
		flex-direction: row;
		// border-bottom:  solid #646566;
		background-color: #FFFFFF;
		
		.course_img {
			margin: 12rpx;
			margin-left: 12rpx;
			width: 60rpx;
			height: 60rpx;
		}
	    
		.course_word {
			margin-top: 16rpx;
		}
	}
</style>
