# QRCode 二维码

二维码能够将文本转换生成二维码的组件，支持自定义配色和 Logo 配置。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/qrcode)。

> 该组件于 1.10.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-qrcode": "tdesign-miniprogram/qrcode/qrcode"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/ZpzwwMmq8a5R)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 01 组件类型

#### 基本用法

```wxml
<t-qrcode value="https://tdesign.tencent.com/" level="M" status="active" />

```
```js
Component({});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-qrcode": "tdesign-miniprogram/qrcode/qrcode"
  }
}

```

#### 带 Icon 的二维码

```wxml
<t-qrcode value="https://tdesign.tencent.com/" icon="https://tdesign.gtimg.com/site/tdesign-logo.png" />

```
```js
Component({});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-qrcode": "tdesign-miniprogram/qrcode/qrcode"
  }
}

```



#### 二维码纠错等级

```wxml
<t-slider value="{{value}}" min="0" max="3" step="1" marks="{{marks}}" bindchange="handleSliderChange" />
<view class="qrcode-content">
  <t-qrcode value="https://tdesign.gtimg.com/site/tdesign-logo.png" level="{{currentLevel}}" status="active" />
</view>

```
```js
Component({
  data: {
    value: 1,
    marks: {
      0: '7%',
      1: '15%',
      2: '25%',
      3: '35%',
    },
    currentLevel: 'M',
  },

  methods: {
    handleSliderChange(e) {
      const { value } = e.detail;
      const levels = ['L', 'M', 'Q', 'H'];
      this.setData({
        value: value,
        currentLevel: levels[value],
      });
    },
  },
});

```
```wxss
.qrcode-content {
  padding: 16px 16px 0;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-qrcode": "tdesign-miniprogram/qrcode/qrcode",
    "t-slider": "tdesign-miniprogram/slider/slider"
  }
}

```

### 02 组件状态

```wxml
<t-qrcode value="https://tdesign.tencent.com/" status="{{'active'}}" bind:refresh="handleRefresh" />

<view class="demo-summary"> expired </view>
<t-qrcode value="https://tdesign.tencent.com/" status="{{'expired'}}" bind:refresh="handleRefresh" />

<view class="demo-summary"> loading </view>
<t-qrcode value="https://tdesign.tencent.com/" status="{{'loading'}}" bind:refresh="handleRefresh" />

<view class="demo-summary"> scanned </view>
<t-qrcode value="https://tdesign.tencent.com/" status="{{'scanned'}}" bind:refresh="handleRefresh" />

```
```js
Component({
  methods: {
    handleRefresh() {
      console.log('Click Refresh');
    },
  },
});

```
```wxss
.demo-summary {
  padding-top: 48rpx;
  padding-bottom: 32rpx;
  box-sizing: border-box;

  line-height: 22px;
  color: var(--bg-color-demo-desc);
  font-size: var(--td-font-size-base, 28rpx);
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-qrcode": "tdesign-miniprogram/qrcode/qrcode"
  }
}

```

### 03 组件样式

#### 二维码颜色

```wxml
<t-qrcode value="https://tdesign.tencent.com/" level="M" status="active" color="#0052D9" bgColor="#fff" />

<view class="demo-summary"> 二维码背景颜色 </view>

<t-qrcode value="https://tdesign.tencent.com/" level="M" status="active" color="#0052D9" bgColor="#D9E1FF" />

```
```js
Component({});

```
```wxss
.demo-summary {
  padding-top: 48rpx;
  padding-bottom: 32rpx;
  box-sizing: border-box;

  line-height: 22px;
  color: var(--bg-color-demo-desc);
  font-size: var(--td-font-size-base, 28rpx);
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-qrcode": "tdesign-miniprogram/qrcode/qrcode"
  }
}

```

#### 二维码尺寸

```wxml
<view class="container">
  <view class="button-group">
    <t-button class="button" variant="text" disabled="{{size <= minSize}}" bindtap="changeSize" data-step="{{ -10 }}">
      - Smaller
    </t-button>
    <view class="line"></view>
    <t-button class="button" variant="text" disabled="{{size >= maxSize}}" bindtap="changeSize" data-step="{{ 10 }}">
      + Larger
    </t-button>
  </view>
  <view class="qrcode-container">
    <t-qrcode size="{{size}}" value="https://tdesign.tencent.com/" />
  </view>
</view>

```
```js
Component({
  data: {
    size: 160,
    minSize: 80,
    maxSize: 240,
  },
  methods: {
    changeSize(e) {
      const newSize = this.data.size + e.currentTarget.dataset.step;
      if (newSize >= this.data.minSize && newSize <= this.data.maxSize) {
        this.setData({ size: newSize });
      }
    },
  },
});

```
```wxss
.container {
  display: flex;
  flex-direction: column;
}

.button-group {
  width: 100%;
  display: flex;
  padding: 0;
  border: 1px solid var(--td-component-border);
  border-radius: 6px;
  margin-bottom: 16px;
  overflow: hidden;
}

.line {
  height: auto;
  width: 1px;
  background-color: var(--td-component-border);
}

.button {
  flex: 1;
  --td-button-border-radius: 0px;
}

.qrcode-container {
  display: flex;
  height: 320px;
  padding: 20px 0;
  justify-content: center;
  align-items: center;
  align-self: stretch;
  background: var(--td-bg-color-secondarycontainer);
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-qrcode": "tdesign-miniprogram/qrcode/qrcode",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```


## FAQ

### 关于二维码纠错等级
纠错等级也叫纠错率，就是指二维码可以被遮挡后还能正常扫描，而这个能被遮挡的最大面积就是纠错率。

通常情况下二维码分为 4 个纠错级别：`L级` 可纠正约 `7%` 错误、`M级` 可纠正约 `15%` 错误、`Q级` 可纠正约 `25%` 错误、`H级` 可纠正约 `30%` 错误。但并不是所有位置都可以缺损，像最明显的三个角上的方框，直接影响初始定位。中间零散的部分是内容编码，可以容忍缺损。当二维码的内容编码携带信息比较少的时候，也就是链接比较短的时候，设置不同的纠错等级，生成的图片不会发生变化。
有关更多信息，可参阅[官方文档](https://www.qrcode.com/zh/about/error_correction)的相关资料

### 生成的二维码无法扫描？
若二维码无法扫码识别，可能是因为链接地址过长导致像素过于密集，可以通过 `size` 配置二维码更大，或者通过短链接服务等方式将链接变短。

### `hidden` 元素中，二维码绘制失败？
当 QRCode 外层使用 `hidden` 包裹，可以通过 `wx:if` 或者重新调用组件的 `init` 方法，确保组件正常渲染（在 t-popup/t-dialog 中同理）。如下：[可参考代码片段](https://developers.weixin.qq.com/s/OUlsk0mq8x6V)

```html
<t-qrcode id="qrcode" />
```

```js
const $qrcode = this.selectComponent('#qrcode');

$qrcode.init();
```
##

## API

### QRCode Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
bg-color | String | - | 二维码背景颜色 | N
borderless | Boolean | false | 是否有边框 | N
color | String | - | 二维码颜色 | N
icon | String | - | 二维码中图片的地址 | N
icon-size | Number / Object | 40 | 二维码中图片的大小。TS 类型：`number \| { width: number; height: number }` | N
level | String | M | 二维码纠错等级。可选项：L/M/Q/H | N
size | Number | 160 | 二维码大小 | N
status | String | active | 二维码状态。可选项：active/expired/loading/scanned。TS 类型：`QRStatus` `type QRStatus = "active" \| "expired" \| "loading" \| "scanned"`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/qrcode/type.ts) | N
value | String | - | 扫描后的文本 | N

### QRCode Events

名称 | 参数 | 描述
-- | -- | --
refresh | \- | 点击"点击刷新"的回调

### QRCode Slots

名称 | 描述
-- | --
status-render | 自定义状态渲染器

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-brand-color-hover | --td-brand-color-hover | -
--td-success-color | --td-success-color | -
