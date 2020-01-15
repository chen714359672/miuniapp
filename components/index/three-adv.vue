<template>
	<view class="d-flex">
		<image :src="threeAdv.big.src" lazy-load style="width: 373upx;height: 530upx;border-right: 2upx solid #F5F5F5;"></image>
		<view class="d-flex flex-column">
			<image :src="threeAdv.smalltop.src" style="width: 375upx;height: 264upx;border-bottom: 2upx solid #F5F5F5;"></image>
			<image :src="threeAdv.smallbottom.src" style="width: 375upx;height: 264upx;"></image>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			threeAdv:Object
		},
	}
</script>

<style>
</style>
