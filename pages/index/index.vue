<template>
	<view class="content">
		<view class="text-center mrg50T"><text class="title">区间选择滑块/范围选择滑块</text></view>

		<view class="part part1 mrg50T">
			<view class="title">1. 默认示例：</view>
			<view class="text-center mrg10T">
				<text>区间：</text>
				<text>{{ rangeValues[0] }}</text>
				<text>~</text>
				<text>{{ rangeValues[1] }}</text>
			</view>
			<view class="rowBox mrg50T">
				<view class="sliderBox">
					<RangeSlider
						:width="slideWidth"
						:height="slideHeight"
						:blockSize="slideBlockSize"
						:min="slideMin"
						:max="slideMax"
						:values="rangeValues"
						:step="step"
						:liveMode="isLiveMode"
						@rangechange="onRangeChange"
					>
						<view slot="minBlock" class="range-slider-block"></view>
						<!-- 左边滑块的内容 -->
						<view slot="maxBlock" class="range-slider-block"></view>
						<!-- 右边滑块的内容 -->
					</RangeSlider>
				</view>
			</view>

			<button @tap="test" class="testBtn">手动设置为10~60</button>
		</view>

		<view class="part part2 mrg50T">
			<view class="title">2. 示例：将原始数据格式化为时间显示</view>
			<view class="text-center mrg50T">
				<RangeSlider
					:width="slideWidth"
					:height="slideHeight"
					:blockSize="slideBlockSize"
					:min="timeMinValue"
					:max="timeMaxValue"
					:activeColor="'#E68B28'"
					:values="rangeValues2"
					@rangechange="onRangeChange2"
				>
					<view slot="minBlock" class="range-slider-block"></view>
					<!-- 左边滑块的内容 -->
					<view slot="maxBlock" class="range-slider-block"></view>
					<!-- 右边滑块的内容 -->
				</RangeSlider>
				<text class="plan-unit">{{ serTime }}</text>
			</view>
		</view>

		<view class="part part3 mrg50T">
			<view class="title">3. 示例：页面第三个滑块</view>

			<view class="text-center mrg10T">
				<text>区间：</text>
				<text>{{ rangeValues3[0] }}</text>
				<text>~</text>
				<text>{{ rangeValues3[1] }}</text>
			</view>

			<view class="text-center mrg50T">
				<RangeSlider
					:width="slideWidth"
					:height="slideHeight"
					:blockSize="slideBlockSize"
					:min="slideMin"
					:max="slideMax"
					:values="rangeValues3"
					:step="step"
					:liveMode="isLiveMode"
					@rangechange="onRangeChange3"
				>
					<view slot="minBlock" class="range-slider-block"></view>
					<!-- 左边滑块的内容 -->
					<view slot="maxBlock" class="range-slider-block"></view>
					<!-- 右边滑块的内容 -->
				</RangeSlider>
			</view>
		</view>

		<text class="tips">修改自：https://github.com/Money888/wechat-rangeslider</text>
	</view>
</template>

<script>
import RangeSlider from '../../components/range-slider/range-slider.vue';

export default {
	data() {
		return {
			// rangeValues: [2, 5], //当前区间值
			// slideWidth: 350, //宽度
			// slideHeight: 80,  //高度
			// slideBlockSize: 56, //圆形按钮大小
			// slideMin: 0,  //slider最小值
			// slideMax: 12,  //slider最大值

			rangeValues: [4, 5.2],
			slideWidth: 350,
			slideHeight: 80,
			slideBlockSize: 30,
			slideMin: 0,
			slideMax: 10,
			isLiveMode: true,
			step: 0.1,
			//
			timeMinValue: 0,
			timeMaxValue: 10,

			rangeValues2: [1, 6],
			serTime: '02:24:00-14:24:00',

			rangeValues3: [3, 5]
		};
	},
	components: {
		RangeSlider
	},
	onLoad() {
		console.log('index onload');
	},
	methods: {
		pad: function(num, n) {
			return Array(n - ('' + num).length + 1).join(0) + num;
		},
		onRangeChange: function(e) {
			this.rangeValues = [e.minValue, e.maxValue];

			console.log(this.rangeValues);
			console.log(JSON.stringify(e));
		},
		test: function() {
			this.rangeValues = [4.2, 6.6];
		},
		onRangeChange2: function(e) {
			let startTime = this.formatTimeBySliderValue(e.originalValue.minValue);
			let endTime = this.formatTimeBySliderValue(e.originalValue.maxValue);
			this.serTime = startTime + '-' + endTime;
		},
		onRangeChange3: function(e) {
			this.rangeValues3 = [e.minValue, e.maxValue];
		},
		formatTimeBySliderValue(value) {
			//按比例，将滑块上面的数值进行转换为时间形式
			//转换为分钟数
			let minutes = (24 * 60 * value) / this.slideMax;
			//转换为小时数
			let hours = parseInt(minutes / 60);
			//剩余分钟数
			let minutes_min = parseInt(minutes % 60);
			return '' + this.pad(hours, 2) + ':' + this.pad(minutes_min, 2) + ':' + '00';
		}
	}
};
</script>

<style lang="scss">
view {
	display: flex;
}

.content {
	justify-content: center;
	flex-direction: column;
}

.sliderBox {
	justify-content: center;
	margin-right: 50rpx;
}

.text-center {
	justify-content: center;
}

.rowBox {
	flex-direction: row;
	align-items: center;
	justify-content: center;
}

.mrg10T {
	margin-top: 10rpx;
}

.tips {
	color: #999;
	font-size: 24rpx;
	text-align: center;
	margin-top: 100rpx;
}

.testBtn {
	margin-top: 50rpx;
}

.part {
	flex-direction: column;
	justify-content: center;
	border-top: 1rpx solid #ccc;
	padding-top: 50rpx;
	.title {
		font-size: 32rpx;
		padding: 0 30rpx;
	}
}

.part2 {
	margin-top: 100rpx;
}
</style>
