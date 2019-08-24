<template>
	<view class="content">
		<view class="text-center mrg50T"><text class="title">区间选择滑块/范围选择滑块</text></view>

		<view class="part1 mrg50T">
			<view class="title">1. 默认示例：</view>
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

				<view class="text-center">
					<text>区间：</text>
					<text>{{ rangeValues[0] }}</text>
					<text>~</text>
					<text>{{ rangeValues[1] }}</text>
				</view>
			</view>

			<button @tap="test" class="testBtn">手动设置为10~60</button>
		</view>

		<view class="part2 mrg50T">
			<view class="title">2. 示例：将原始数据格式化为时间显示</view>
			<view class="text-center mrg50T">
				<RangeSlider
					:width="slideWidth"
					:height="slideHeight"
					:blockSize="slideBlockSize"
					:min="slideMin"
					:max="slideMax"
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

			minValue: 0,
			maxValue: 24,
			rangeValues: [0, 1],
			slideWidth: 350,
			slideHeight: 80,
			slideBlockSize: 56,
			slideMin: 0,
			slideMax: 3,
			//
			rangeValues2: [0, 10],
			serTime: '00:00:00-10:00:00',
			time: '13.5小时',
			step:0.1,
			isLiveMode:true,
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
		},
		test: function() {
			this.rangeValues = [10, 60];
		},
		onRangeChange2: function(e) {
			let startTime = this.formatTimeBySliderValue(e.originalValue.minValue);
			let endTime = this.formatTimeBySliderValue(e.originalValue.maxValue);
			this.serTime = startTime + '-' + endTime;
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
	display: flex
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

.testBtn {
	margin-top: 50upx;
}

.part1,
.part2 {
	flex-direction: column;
	justify-content: center;
	border-top: 1upx solid #ccc;
	padding-top: 50upx;
	.title {
		font-size: 32upx;
		padding: 0 30upx;
	}
}

.part2 {
	margin-top: 100upx;
}
</style>
