<template>
	<view>
		<!-- 商品详情大图 -->
		<swiper-image :swipers="banners" height="750" preview></swiper-image>
		
		<!-- 基础详情 -->
		<base-info :detail="detail"></base-info>
		
		<!-- 滚动商品特性 -->
		<scroll-attrs :baseAttrs="baseAttrs"></scroll-attrs>
		
		<!-- 属性选择 -->
		<view class="p-2">
			<view class="rounded border bg-light-secondary">
				<uni-list-item>
					<view class="d-flex">
						<text class="mr-2 text-muted">已选</text>
						<text>火焰红 64G 标配</text>
					</view>
				</uni-list-item>
				<uni-list-item>
					<view class="d-flex">
						<text class="mr-2 text-muted">配送</text>
						<text class="mr-2">北京 东城区</text>
						<text class="main-text-color">现配</text>
					</view>
				</uni-list-item>
				<uni-list-item>
					<view class="d-flex a-center">
						<view class="text-muted font d-flex a-center mr-2">
							<view class="iconfont icon-finish main-text-color"></view>
							小米自营
						</view>
						<view class="text-muted font d-flex a-center mr-2">
							<view class="iconfont icon-finish main-text-color"></view>
							小米发货
						</view>
						<view class="text-muted font d-flex a-center mr-2">
							<view class="iconfont icon-finish main-text-color"></view>
							七天无理由退货
						</view>
					</view>
				</uni-list-item>
			</view>
		</view>
		
	</view>
</template>

<script>
	import swiperImage from '@/components/index/swiper-image.vue';
	import baseInfo from '@/components/detail/base-info.vue'
	import scrollAttrs from '@/components/detail/scroll-attrs.vue'
	import uniListItem from '@/components/uni-ui/uni-list-item/uni-list-item.vue'
	export default {
		components:{
			swiperImage,
			baseInfo,
			scrollAttrs,
			uniListItem
		},
		data() {
			return {
				banners:[
					{src:"../../static/images/demo/demo10.jpg"},
					{src:"../../static/images/demo/demo10.jpg"}
				],
				detail:{
					title:"小米",
					desc:'水水水水水水水水水水水水',
					pprice:333
				},
				baseAttrs:[
					{icon:"icon-cpu",title:"CPU",desc:"蛟龙845八核"},
					{icon:"icon-cpu",title:"CPU",desc:"蛟龙845八核"},
					{icon:"icon-cpu",title:"CPU",desc:"蛟龙845八核"},
					{icon:"icon-cpu",title:"CPU",desc:"蛟龙845八核"},
					{icon:"icon-cpu",title:"CPU",desc:"蛟龙845八核"}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
