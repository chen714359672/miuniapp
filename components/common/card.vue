<template>
	<view class="card">
		<view v-if="showhead" class=" p-2  main-border-color" :class="getHeadClass">
			<slot name="title">
				<text v-if="headTitle" class="font-md" :class="headTitleWeight?'font-weight':''">{{headTitle}}</text>
			</slot>
		</view>
		<view :class="getBodyClass">
			<image v-if="bodyCover" :src="bodyCover" mode="widthFix"></image>
			<slot></slot>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			//头部标题
			headTitle:String,
			//封面图
			bodyCover:String,
			//是否显示头部
			showhead:{
				type:Boolean,
				default:true
			},
			//是否显示下边线
			headBorderBottom:{
				type:Boolean,
				default:true
			},
			//是否给body给padding
			bodyPadding:{
				type:Boolean,
				default:true
			},
			//标题是否加粗
			headTitleWeight:{
				type:Boolean,
				default:true
			}
		},
		computed: {
			getHeadClass() {
				let BorderBottom = this.headBorderBottom ? 'border-bottom' : ''
				return `${BorderBottom}`
			},
			getBodyClass(){
				let bodyPadding = this.bodyPadding ? 'p-2' : ''
				return `${bodyPadding}`
			},
		},
	}
</script>

<style>
</style>
