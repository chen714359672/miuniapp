<template>
	<view class="d-flex border-top border-light-secondary" style="height: 100%;box-sizing:border-box;">
		
		<loading :show="showLoading"></loading>
		
		<scroll-view scroll-y style="flex: 1;height: 100%;" class="border-right border-light-secondary" id="leftScroll" :scroll-top="leftScrollTop">
			<view
				class="border-bottom border-light-secondary py-1 left-scroll-item"
				hover-class="bg-light-secondary"
				v-for="(item, index) in cate"
				:key="index"
				@tap="changeCate(index)"
			>
				<view class="py-1 font-md text-muted text-center" :class="activeIndex === index ? 'class-active' : ''">{{ item.name }}</view>
			</view>
		</scroll-view>
		<scroll-view scroll-y style="flex: 3.5;height: 100%;" :scroll-top="rightScrollTop" :scroll-with-animation="true" @scroll="onRightScroll">
			<view class="row right-scroll-item" v-for="(item, index) in list" :key="index">
				<view class="span24-8 text-center py-2" v-for="(item2, index2) in item.list" :key="index2">
					<image :src="item2.src"></image>
					<text class="d-block">{{ item2.name }}</text>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			showLoading:true,
			activeIndex: 0,
			cate: [],
			list: [
				{
					list: []
				}
			],
			leftDomsTop: [],
			rightDomsTop: [],
			rightScrollTop: 0,
			cateItemHeight: 0,
			leftScrollTop: 0
		};
	},
	onLoad() {
		this.getData();
	},
	onReady() {
		const query = uni.createSelectorQuery().in(this);
		query
			.selectAll('.left-scroll-item')
			.fields(
				{
					size: true,
					rect: true
				},
				data => {
					this.leftDomsTop = data.map(v => {
						this.cateItemHeight = v.height;
						return v.top;
					});
				}
			)
			.exec();
		query
			.selectAll('.right-scroll-item')
			.boundingClientRect(data => {
				this.rightDomsTop = data.map(v => v.top);
			})
			.exec();
	},
	watch: {
		activeIndex(newValue, oldValue) {
			//获取scroll-view高度，scrollTop
			const query = uni.createSelectorQuery().in(this);
			query
				.select('#leftScroll')
				.fields(
					{
						size: true,
						scrollOffset: true
					},
					data => {
						let H = data.height;
						let ST = data.scrollTop;
						//下边
						if ((this.leftDomsTop[newValue] + this.cateItemHeight) > (H + ST)) {
							return this.leftScrollTop = this.leftDomsTop[newValue] + this.cateItemHeight - H;
						}
						//上边
						if (ST > this.cateItemHeight) {
							this.leftScrollTop = this.leftDomsTop[newValue];
						}
					}
				)
				.exec();
		}
	},
	methods: {
		//获取节点信息
		getElInfo(obj = {}){
			let option = {
				size: obj.size ? true : false,
				rect: obj.rect ? true : false
			}
		},
		//点击左边分类
		changeCate(index) {
			this.activeIndex = index;
			//右边scroll滚动到对应区块
			this.rightScrollTop = this.rightDomsTop[index];
		},
		//监听右边滚动事件
		async onRightScroll(e) {
			//匹配当前scroll所处的索引
			this.rightDomsTop.forEach((v, k) => {
				if (v < e.detail.scrollTop) {
					this.activeIndex = k;
					return false;
				}
			});
		},
		getData() {
			for (let i = 0; i < 20; i++) {
				this.cate.push({
					name: '分类' + i
				});
				this.list.push({
					list: []
				});
			}
			for (let i = 0; i < this.list.length; i++) {
				for (let j = 0; j < 20; j++) {
					this.list[i].list.push({
						src: '/static/images/demo/cate_03.png',
						name: `分类${i}-商品${j}`
					});
				}
			}
			this.$nextTick(() => {
				this.showLoading = false
			})
		}
	}
};
</script>

<style>
.class-active {
	border-left: 8upx solid #fd6801;
	color: #fd6801 !important;
}
</style>
