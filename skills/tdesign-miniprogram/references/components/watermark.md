# Watermark 水印

给页面的某个区域加上水印。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/watermark)。

> 该组件于 1.11.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-watermark": "tdesign-miniprogram/watermark/watermark"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/fiE2LNmk8C5q)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 组件类型

#### 文字水印

```wxml
<t-watermark watermark-content="{{watermark}}" y="{{56}}" x="{{56}}" width="{{68}}" height="{{52}}">
  <view style="width: 100%; height: 340px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: { text: '文字水印' },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

#### 图片水印

```wxml
<t-watermark watermark-content="{{watermark}}" width="{{120}}" height="{{20}}" x="{{56}}" y="{{76}}">
  <view style="width: 100%; height: 300px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: { url: 'https://tdesign.gtimg.com/starter/brand-logo-light.png' },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

#### 图片灰阶水印

```wxml
<t-watermark watermark-content="{{watermark}}" width="{{120}}" height="{{20}}" x="{{56}}" y="{{76}}" alpha="{{0.3}}">
  <view style="width: 100%; height: 300px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: {
      url: 'https://tdesign.gtimg.com/starter/brand-logo-light.png',
      isGrayscale: true,
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

#### 多行图文水印

```wxml
<t-watermark
  watermark-content="{{watermark}}"
  line-space="{{24}}"
  x="{{56}}"
  y="{{76}}"
  width="{{120}}"
  height="{{20}}"
  alpha="{{0.3}}"
>
  <view style="width: 100%; height: 300px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: [
      { text: '水印文本', fontColor: 'black' },
      { url: 'https://tdesign.gtimg.com/starter/brand-logo-light.png' },
    ],
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

#### 多行图文灰阶水印

```wxml
<t-watermark
  watermark-content="{{watermark}}"
  line-space="{{24}}"
  x="{{56}}"
  y="{{76}}"
  width="{{120}}"
  height="{{20}}"
  alpha="{{0.3}}"
>
  <view style="width: 100%; height: 300px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: [
      { text: '水印文本', fontColor: 'black' },
      { url: 'https://tdesign.gtimg.com/starter/brand-logo-light.png', isGrayscale: true },
    ],
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

#### 运动文字水印

```wxml
<t-watermark watermark-content="{{watermark}}" width="{{120}}" height="{{60}}" y="{{200}}" x="{{210}}" movable>
  <view style="width: 100%; height: 300px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: { text: '文字水印' },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

#### 运动图片水印

```wxml
<t-watermark watermark-content="{{watermark}}" x="{{100}}" y="{{140}}" width="{{120}}" height="{{30}}" movable>
  <view style="width: 100%; height: 300px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: { url: 'https://tdesign.gtimg.com/site/baseLogo-light.png' },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```

### 不同布局的水印
通过设置 layout 使用不同的布局。

```wxml
<view class="demo-desc" style="margin-bottom: 32rpx">Rectangular Grid 矩形布局</view>
<t-watermark watermark-content="{{watermark}}" y="{{56}}" x="{{56}}" width="{{68}}" height="{{52}}">
  <view style="width: 100%; height: 340px" />
</t-watermark>

<view class="demo-desc" style="margin-bottom: 32rpx">Hexagonal Grid 六边形网格</view>
<t-watermark watermark-content="{{watermark}}" y="{{56}}" x="{{56}}" width="{{68}}" height="{{52}}" layout="hexagonal">
  <view style="width: 100%; height: 340px" />
</t-watermark>

```
```js
Component({
  data: {
    watermark: { text: '文字水印' },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-watermark": "tdesign-miniprogram/watermark/watermark"
  }
}

```


## API

### Watermark Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
alpha | Number | 1 | 水印整体透明度，取值范围 [0-1] | N
content | String | - | 水印所覆盖的内容节点 | N
height | Number | - | 水印高度 | N
is-repeat | Boolean | true | 水印是否重复出现 | N
layout | String | rectangular | 水印的布局方式，rectangular：矩形，即横平竖直的水印；hexagonal：六边形，即错位的水印。可选项：rectangular/hexagonal | N
line-space | Number | 16 | 行间距，只作用在多行（`content` 配置为数组）情况下 | N
movable | Boolean | false | 水印是否可移动 | N
move-interval | Number | 3000 | 水印发生运动位移的间隙，单位：毫秒 | N
offset | Array | - | 水印在画布上绘制的水平和垂直偏移量，正常情况下水印绘制在中间位置，即 `offset = [gapX / 2, gapY / 2]`。TS 类型：`Array<number>` | N
removable | Boolean | true | 水印是否可被删除 | N
rotate | Number | -22 | 水印旋转的角度，单位 ° | N
watermark-content | Object / Array | - | 水印内容，需要显示多行情况下可配置为数组。TS 类型：`WatermarkText\|WatermarkImage\|Array<WatermarkText\|WatermarkImage>` | N
width | Number | - | 水印宽度 | N
x | Number | - | 水印之间的水平间距 | N
y | Number | - | 水印之间的垂直间距 | N
z-index | Number | - | 水印元素的 `z-index`，默认值写在 CSS 中 | N

### Watermark Slots

名称 | 描述
-- | --
\- | 默认插槽，作用同 `content` 插槽
content | 自定义 `content` 显示内容

### WatermarkText

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
font-color | String | rgba(0,0,0,0.1) | 水印文本文字颜色 | N
font-family | String | - | 水印文本文字字体 | N
font-size | Number | 16 | 水印文本文字大小 | N
font-weight | String | normal | 水印文本文字粗细。可选项：normal/lighter/bold/bolder | N
text | String | - | 水印文本内容 | N

### WatermarkImage

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
is-grayscale | Boolean | false | 水印图片是否需要灰阶显示 | N
url | String | - | 水印图片源地址，为了显示清楚，建议导出 2 倍或 3 倍图 | N

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--watermark-left-0 | --watermark-left-0 | -
--watermark-left-25 | --watermark-left-25 | -
--watermark-left-50 | --watermark-left-50 | -
--watermark-left-75 | --watermark-left-75 | -
--watermark-top-0 | --watermark-top-0 | -
--watermark-top-25 | --watermark-top-25 | -
--watermark-top-50 | --watermark-top-50 | -
--watermark-top-75 | --watermark-top-75 | -
