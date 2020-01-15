<template>
	<view>
		<!-- 顶部选项卡 -->
		<scroll-view scroll-x class="border-bottom scroll-row" style="height: 80rpx;" :scroll-into-view="srcollinto" :scroll-with-animation="true">
			<view
				class="scroll-row-item px-3"
				@click="changeTab(index)"
				style="height: 80rpx;line-height: 80rpx;"
				v-for="(item, index) in tabBars"
				:key="index"
				:class="tabIndex === index ? 'main-text-color border-bottom' : ''"
				:id="'tab' + index"
			>
				<text class="font-md">{{ item.name }}</text>
			</view>
		</scroll-view>

		<swiper :current="tabIndex" :style="'height:' + scrollH + 'px;'" :duration="150" @change="onChangeTab">
			<swiper-item v-for="(item, index) in newsitems" :key="index">
				<scroll-view scroll-y="true" :style="'height:' + scrollH + 'px;'">
					<block v-for="(list, listIndex) in item.list" :key="listIndex">
						<!-- 轮播图组件 -->
						<swiper-image v-if="list.type === 'swipers'" :swipers="list.data" />

						<template v-else-if="list.type === 'indexnavs'">
						<!-- 首页分类 -->
						<index-nav :indexnavs="list.data" />
						<!-- 全局分割线 -->
						<divider />
						</template>

						<template v-else-if="list.type === 'threeAdv'">
						<!-- 三图广告 -->
						<three-adv :threeAdv="list.data" />
						<divider />
						</template>

						<!-- 大图广告位 -->
						<card>
							<block slot="title">每日精选</block>
							<image src="/static/images/bg.jpg" mode="widthFix"></image>
						</card>

						<!-- 公共列表组件 -->
						<view class="row j-sb">
							<block v-for="(item2, index2) in commonList" :key="index2"><common-list :item="item2" :index="index2"></common-list></block>
						</view>
					</block>
					
					<!-- 上拉加载更多 -->
					<view class="d-flex a-center j-center text-light-muted font-md py-3">
						上拉加载更多
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
import swiperImage from '@/components/index/swiper-image.vue';
import indexNav from '@/components/index/index-nav.vue';
import threeAdv from '@/components/index/three-adv.vue';
import card from '@/components/common/card.vue';
import commonList from '@/components/common/common-list.vue';
export default {
	components: {
		swiperImage,
		indexNav,
		threeAdv,
		card,
		commonList
	},
	data() {
		return {
			srcollinto: 'tab0',
			scrollH: 500,
			tabIndex: 0,
			tabBars: [
				{
					name: '推荐'
				},
				{
					name: '关注'
				},
				{
					name: '体育'
				},
				{
					name: '热点'
				},
				{
					name: '财经'
				},
				{
					name: '推荐'
				},
				{
					name: '关注'
				},
				{
					name: '体育'
				},
				{
					name: '热点'
				},
				{
					name: '财经'
				}
			],

			newsitems: [
				{
					name: '推荐',
					list: [
						{
							type: 'swipers',
							data: [{ src: '../../static/images/demo/demo4.jpg' }, { src: '../../static/images/demo/demo4.jpg' }, { src: '../../static/images/demo/demo4.jpg' }]
						}
					]
				},
				{
					name: '关注',
					list: [
						{
							type: 'indexnavs',
							data: [
								{ src: '/static/images/indexnav/1.png', text: '新品发布' },
								{ src: '/static/images/indexnav/2.gif', text: '小米众筹' },
								{ src: '/static/images/indexnav/3.gif', text: '以旧换新' },
								{ src: '/static/images/indexnav/4.gif', text: '一分换团' },
								{ src: '/static/images/indexnav/5.gif', text: '超值特卖' },
								{ src: '/static/images/indexnav/6.gif', text: '小米秒杀' },
								{ src: '/static/images/indexnav/7.gif', text: '真心想要' },
								{ src: '/static/images/indexnav/8.gif', text: '电视热卖' },
								{ src: '/static/images/indexnav/9.gif', text: '家电热卖' },
								{ src: '/static/images/indexnav/10.gif', text: '米粉卡' }
							]
						}
					]
				},
				{
					name: '体育',
					list: [
						{
							type: 'threeAdv',
							data: {
								big: { src: '/static/images/demo/demo1.jpg' },
								smalltop: { src: '/static/images/demo/demo2.jpg' },
								smallbottom: { src: '/static/images/demo/demo2.jpg' }
							}
						}
					]
				},
				{
					name: '热点'
				},
				{
					name: '财经'
				},
				{
					name: '推荐'
				},
				{
					name: '关注'
				},
				{
					name: '体育'
				},
				{
					name: '热点'
				},
				{
					name: '财经'
				}
			],
			commonList: [
				{
					cover: '/static/images/demo/list/1.jpg',
					tilte: '米家空调',
					desc: '1.5匹变频',
					oprice: 2699,
					pprice: 1399
				},
				{
					cover: '/static/images/demo/list/1.jpg',
					tilte: '米家空调',
					desc: '1.5匹变频',
					oprice: 2699,
					pprice: 1399
				}
			]
		};
	},
	created(){
		
	},
	onNavigationBarSearchInputClicked(){
		uni.navigateTo({
			url: "../search/search"
		})
	},
	onLoad() {
		//获取可视区高度
		uni.getSystemInfo({
			success: res => {
				this.scrollH = res.windowHeight - uni.upx2px(82);
			}
		});
	},
	methods: {
		//切换选项卡
		changeTab(index) {
			if (this.tabIndex === index) {
				return;
			}
			this.tabIndex = index;
			this.srcollinto = 'tab' + index;
			console.log(this.srcollinto);
		},
		//监听滑动列表
		onChangeTab(e) {
			this.changeTab(e.detail.current);
		}
	}
};
</script>

<style></style>
