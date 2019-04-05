<template>
	<view class="content">
		<view class="text-center mrg50T">
			<text class="title">区间选择滑块/范围选择滑块</text>
		</view>

		<view class="rowBox mrg50T">
			<view class="sliderBox">
				<RangeSlider :width='slideWidth' :height='slideHeight' :blockSize='slideBlockSize' :min='slideMin' :max='slideMax'
				 :values='rangeValues' @rangechange='onRangeChange'>
					<view slot='minBlock' class='range-slider-block'></view> //左边滑块的内容
					<view slot='maxBlock' class='range-slider-block'></view> //右边滑块的内容
				</RangeSlider>
			</view>

			<view class="text-center">
				<text>区间：</text>
				<text>{{rangeValues[0]}}</text>
				<text>~</text>
				<text>{{rangeValues[1]}}</text>
			</view>
		</view>

		<button @tap="test" class="testBtn">手动设置为10~60</button>

		<text class="tips">修改自：https://github.com/Money888/wechat-rangeslider</text>
	</view>
</template>

<script>
	import RangeSlider from '../../components/range-slider/range-slider.vue';

	export default {
		data() {
			return {
				rangeValues: [0, 80], //当前区间值
				slideWidth: 350, //宽度
				slideHeight: 80,  //高度
				slideBlockSize: 56, //圆形按钮大小
				slideMin: 0,  //slider最小值
				slideMax: 100,  //slider最大值
			}
		},
		components: {
			RangeSlider
		},
		onLoad() {

		},
		methods: {
			onRangeChange: function(e) {
				this.rangeValues =  [ Math.round(e.minValue),  Math.round(e.maxValue)];
			},
			test:function()
			{
				this.rangeValues = [10,60];
			}
		}
	}
</script>

<style>
	view {
		display: flex;
	}

	.content {
		justify-content: center;
		flex-direction: column;
	}

	.sliderBox {
		justify-content: center;
		margin-right: 50upx;
	}

	.text-center {
		justify-content: center;
	}

	.rowBox {
		flex-direction: row;
		align-items: center;
		justify-content: center;
	}

	.mrg50T {
		margin-top: 50upx;
	}

	.tips {
		color: #999;
		font-size: 24upx;
		text-align: center;
		margin-top: 100upx;
	}
	
	.testBtn
	{
		margin-top:100upx;
	}
</style>
