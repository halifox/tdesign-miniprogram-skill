# Overlay 遮罩层

通过遮罩层，可以强调部分内容

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/overlay)。

> 该组件于 0.10.0 版本上线，请留意版本
> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-overlay": "tdesign-miniprogram/overlay/overlay"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/K7ypAMmC8L5D)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 基础使用

```wxml
<t-overlay visible="{{visible}}" duration="{{500}}" bind:click="handleOverlayClick" />

<t-button block size="large" theme="primary" variant="outline" bind:tap="handleClick">基础用法</t-button>

```
```js
Component({
  data: {
    visible: false,
  },
  methods: {
    handleClick() {
      this.setData({ visible: true });
    },
    handleOverlayClick(e) {
      this.setData({
        visible: e.detail.visible,
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-overlay": "tdesign-miniprogram/overlay/overlay",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```

## API

### Overlay Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
background-color | String | - | 遮罩层的背景色 | N
duration | Number | 300 | 背景色过渡时间，单位毫秒 | N
prevent-scroll-through | Boolean | true | 防止滚动穿透，即不允许点击和滚动 | N
using-custom-navbar | Boolean | false | 是否使用了自定义导航栏 | N
visible | Boolean | false | 是否展示 | N
z-index | Number | - | 遮罩层级，默认为 11000 | N

### Overlay Events

名称 | 参数 | 描述
-- | -- | --
click | `({ visible: boolean })` | 点击遮罩时触发

### Overlay Slots

名称 | 描述
-- | --
\- | 默认插槽，自定义内容区域内容

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-overlay-bg-color | @mask-active | -
--td-overlay-transition-duration | 300ms | -
--td-overlay-zindex | @z-index-overlay | -
