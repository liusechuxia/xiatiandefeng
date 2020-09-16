<template>
	<view class="container">
		<view class="search-title">
			<text>请输入关键字查询</text>
			<input type="text" value="" class="keyword uni-input" confirm-type="search"
				style="height:40px;"/>
		</view>
		<button type="primary" @click="SearchList()" class="search-btn">查询</button>
		<view class="f-header m-t">
			<image src="/static/temp/h1.png"></image>
			<view class="tit-box">
				<text class="tit">搜索列表</text>
			</view>
			<text class="yticon icon-you"></text>
		</view>		
		<view class="goods-list">
			<view
				v-for="(item, index) in hotList[0].list" :key="index"
				class="guess-item" @click="ToDetail()"
			>
				<view class="image-wrapper">
					<image :src="item.image" mode="aspectFill"></image>
				</view>
				<text class="title clamp">{{item.title}}</text>
				<text class="price">￥{{item.price}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				hotList: [{}, {}]
			}
		},
		
		methods: {
			async SearchList() {
				let carouselList = await this.$api.json('carouselList');
				this.titleNViewBackground = carouselList[0].background;
				this.swiperLength = carouselList.length;
				this.carouselList = carouselList;
				
				let hotList = await this.$api.json('hotList');
				this.hotList = hotList;
			},
			//商品详情
			ToDetail() {
				uni.navigateTo({
					url: '/pages/product/product'
				})
			},			
			
		}
	}
</script>

<style lang="scss">
	.search-title{
		font-size: 16px;
		margin-left: 10px;
		margin-right: 10px;
	}
	.keyword{
		margin-top: 10px;
		border: 1px solid rgba($color: #8a8a8a, $alpha: 0.5);
		border-radius: 5px;
	}
	.search-btn{
		height: 40px;
		margin: 10px 10px 10px 10px;
	}
	.f-header{
		display:flex;
		align-items:center;
		height: 140upx;
		padding: 6upx 30upx 8upx;
		background: #fff;
		image{
			flex-shrink: 0;
			width: 80upx;
			height: 80upx;
			margin-right: 20upx;
		}
		.tit-box{
			flex: 1;
			display: flex;
			flex-direction: column;
		}
		.tit{
			font-size: $font-lg +2upx;
			color: #font-color-dark;
			line-height: 1.3;
		}
		.icon-you{
			font-size: $font-lg +2upx;
			color: $font-color-light;
		}
	}
	.goods-list{
		display:flex;
		flex-wrap:wrap;
		padding: 0 30upx;
		background: #fff;
		.guess-item{
			display:flex;
			flex-direction: column;
			flex: 1;
			max-width: 50%;
			min-width: 40%;
			padding-bottom: 40upx;
			&:nth-child(2n+1){
				margin-right: 20upx;
			}
		}
		.image-wrapper{
			width: 100%;
			height: 330upx;
			border-radius: 3px;
			overflow: hidden;
			image{
				width: 100%;
				height: 100%;
				opacity: 1;
			}
		}
		.title{
			font-size: $font-lg;
			color: $font-color-dark;
			line-height: 80upx;
		}
		.price{
			font-size: $font-lg;
			color: $uni-color-primary;
			line-height: 1;
		}
	}

</style>
