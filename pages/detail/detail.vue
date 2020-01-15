<template>
	<view>
		<!-- 商品详情大图 -->
		<swiper-image :swipers="banners" height="750" preview></swiper-image>
		
		<!-- 基础详情 -->
		<view class="p-2">
			<view class="font-lg">我是标题</view>
			<view class="font text-light-muted mb-3 line-h-sm">
				我是描述
			</view>
			<price>3500</price>
		</view>
	</view>
</template>

<script>
	import swiperImage from '@/components/index/swiper-image.vue';
	import price from '@/components/common/price.vue'
	export default {
		components:{
			swiperImage,
			price
		},
		data() {
			return {
				banners:[
					{src:"../../static/images/demo/demo10.jpg"},
					{src:"../../static/images/demo/demo10.jpg"}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
