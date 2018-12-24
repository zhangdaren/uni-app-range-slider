# uni-app-range-slider
uni-app 区间选择滑块

## 效果图：
![效果图](https://zhangdaren.github.io/uni-app-range-slider/static/preview.png)

## range-slider属性

| 属性名 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| width | Number | 750 | 组件宽度(rpx)|
| height |Number |100 | 组件高度(rpx) |
| block-size | Number | 50 | 滑块大小(rpx) |
| bar-height | Number | 10 | 进度条高度(rpx) |
| background-color | String | #e9e9e9 | 进度条背景色 |
| active-color | String | #1aad19 | 已选择的颜色 |
| min | Number | 0 | 最小值 |
| max |Number | 100 | 最大值 |
| values |Array| [0,100] | 当前区间值 |
| bindrangechange | EventHandle | |完成一次拖动后触发的事件，event.detail = {minValue: value1,maxValue:value2} |



修改自：
https://github.com/Money888/wechat-rangeslider


