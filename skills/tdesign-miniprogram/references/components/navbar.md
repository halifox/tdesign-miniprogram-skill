# Navbar 导航栏

用于不同页面之间切换或者跳转，位于内容区的上方，系统状态栏的下方。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/navbar)。

> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-navbar": "tdesign-miniprogram/navbar/navbar",
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/XmyPWMmX8D5A)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"


### 基础导航栏

```wxml
<view class="block">
  <t-navbar title="标题文字" fixed="{{false}}" placeholder t-class-title="nav-title" />
</view>

<view class="block">
  <t-navbar class="block" title="标题文字" fixed="{{false}}" left-arrow bind:go-back="handleBack" />
</view>

```
```js
Component({
  methods: {
    handleBack() {
      console.log('go back');
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-navbar": "tdesign-miniprogram/navbar/navbar"
  }
}

```

### 胶囊样式导航栏

```wxml
<t-navbar fixed="{{false}}" title="标题文字">
  <view slot="capsule" class="custom-capsule">
    <t-icon
      size="40rpx"
      bind:tap="onBack"
      aria-role="button"
      aria-label="返回"
      name="chevron-left"
      class="custom-capsule__icon back"
    />
    <t-icon
      size="40rpx"
      bind:tap="onGoHome"
      aria-role="button"
      aria-label="首页"
      name="home"
      class="custom-capsule__icon home"
    />
  </view>
</t-navbar>

```
```js
Component({
  methods: {
    onBack() {
      wx.navigateBack();
    },
    onGoHome() {
      wx.reLaunch({
        url: '/pages/home/home',
      });
    },
  },
});

```
```wxss
.custom-capsule {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.custom-capsule__icon {
  flex: 1;
  position: relative;
}

.custom-capsule__icon.home:before {
  content: '';
  display: block;
  position: absolute;
  left: -1px;
  top: 50%;
  transform: translateY(-50%);
  width: 1px;
  height: 18px;
  background: #e7e7e7;
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-navbar": "tdesign-miniprogram/navbar/navbar",
    "t-icon": "tdesign-miniprogram/icon/icon"
  }
}

```

### 带搜索导航栏

```wxml
<t-navbar fixed="{{false}}" leftIcon="slot">
  <view class="search-box" slot="left">
    <t-search shape="round" placeholder="搜索内容" />
  </view>
</t-navbar>

```
```js
Component({});

```
```wxss
.search-box {
  --td-search-height: 32px;
  --td-search-font: var(--td-font-body-medium);
  --td-search-icon-size: 40rpx;
  width: 252px;
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-navbar": "tdesign-miniprogram/navbar/navbar",
    "t-search": "tdesign-miniprogram/search/search"
  }
}

```

### 带图片导航栏

```wxml
<t-navbar fixed="{{false}}">
  <view slot="left">
    <t-image
      t-class="custom-image"
      src="{{theme === 'dark' ? 'https://tdesign.gtimg.com/mobile/demos/image-dark.png' : 'https://tdesign.gtimg.com/mobile/demos/logo-light.png'}}"
      aria-label="导航栏图片"
    />
  </view>
</t-navbar>

```
```js
import themeChangeBehavior from 'tdesign-miniprogram/mixins/theme-change';

Component({
  behaviors: [themeChangeBehavior],
});

```
```wxss
.custom-image {
  height: 24px;
  width: 87px;
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-navbar": "tdesign-miniprogram/navbar/navbar",
    "t-image": "tdesign-miniprogram/image/image"
  }
}

```

### 组件样式

```wxml
<view class="block">
  <t-navbar fixed="{{false}}" left-arrow title="标题居中" />
</view>

<t-navbar fixed="{{false}}" left-arrow>
  <view slot="left" class="custom-title">标题左对齐</view>
</t-navbar>

<view class="demo-desc">标题尺寸</view>

<t-navbar fixed="{{false}}" left-arrow>
  <text class="left-text" slot="left" bind:tap="onBack">返回</text>
</t-navbar>
<view class="header-title">大标题尺寸</view>

```
```js
Component({
  methods: {
    onBack() {
      wx.navigateBack();
    },
  },
});

```
```wxss
.custom-title {
  margin-left: 8px;
  font-size: 18px;
  font-weight: 600;
}

.block {
  display: block;
  margin-bottom: 48rpx;
}

.demo-desc {
  margin-top: 48rpx;
  margin-bottom: 32rpx;
}

.left-text {
  display: block;
  margin-left: 4px;
  font-size: 16px;
}

.header-title {
  font-size: 28px;
  line-height: 36px;
  padding: 8rpx 32rpx 16rpx;
  background-color: var(--td-bg-color-container);
  font-weight: 600;
  color: var(--td-text-color-primary);
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-navbar": "tdesign-miniprogram/navbar/navbar"
  }
}

```

### 自定义颜色

```wxml
<t-navbar class="custom-navbar" fixed="{{false}}" left-arrow title="标题文字" />

```
```js
Component({});

```
```wxss
.custom-navbar {
  --td-navbar-color: #fff;
  --td-navbar-bg-color: #0052d9;
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-navbar": "tdesign-miniprogram/navbar/navbar"
  }
}

```

## API

### Navbar Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
animation | Boolean | true | 是否添加动画效果 | N
background | String | - | 已废弃。背景 | N
delta | Number | 1 | 后退按钮后退层数，含义参考 [wx.navigateBack](https://developers.weixin.qq.com/miniprogram/dev/api/route/wx.navigateBack.html)，特殊的，传入 0 不会发生执行 wx.navigateBack | N
fixed | Boolean | true | 是否固定在顶部 | N
home-icon | String | - | 已废弃。首页图标地址。值为 '' 或者 undefined 则表示不显示返回图标，值为 'circle' 表示显示默认图标，值为 'slot' 表示使用插槽渲染，值为其他则表示图标地址 | N
is-hidden-in-special-scene | Boolean | false | `1.15.2`。【实验】是否销毁导航栏，仅场景值为 1433、1434、1177、1175 时有效 | N
left-arrow | Boolean | false | `0.26.0`。是否展示左侧箭头 | N
left-icon | String | - | 已废弃。左侧图标地址，值为 '' 或者 undefined 则表示不显示返回图标，值为 'arrow-left' 表示显示返回图标，值为 'slot' 表示使用插槽渲染，值为其他则表示图标地址 | N
placeholder | Boolean | false | `1.12.1`。固定在顶部时是否开启占位 | N
safe-area-inset-top | Boolean | true | 是否开启顶部安全区适配 | N
title | String | - | 页面标题 | N
title-max-length | Number | - | 标题文字最大长度，超出的范围使用 `...` 表示 | N
visible | Boolean | true | 是否显示 | N
z-index | Number | 1 | `1.12.1`。导航条层级 | N

### Navbar Events

名称 | 参数 | 描述
-- | -- | --
complete | \- | navigateBack 执行完成后触发（失败或成功均会触发）
fail | \- | navigateBack 执行失败后触发
go-back | \- | 点击左侧箭头时触发
go-home | \- | 已废弃。点击 Home 触发
success | \- | navigateBack 执行成功后触发

### Navbar Slots

名称 | 描述
-- | --
capsule | 左侧胶囊区域
left | `0.26.0`。左侧内容区域
title | 自定义 `title` 显示内容

### Navbar External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-capsule | 左侧胶囊区域样式类
t-class-center | 中间内容样式类
t-class-home-icon | 首页图标样式类
t-class-left | 左侧内容样式类
t-class-left-icon | 左侧图标样式类
t-class-nav-btn | 导航按钮样式类
t-class-title | 标题样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-navbar-padding-top | 20px | -
--td-navbar-right | 95px | -
--td-navbar-background | @navbar-bg-color | -
--td-navbar-bg-color | @bg-color-container | -
--td-navbar-capsule-border-color | @border-level-1-color | -
--td-navbar-capsule-border-radius | 16px | -
--td-navbar-capsule-height | 32px | -
--td-navbar-capsule-width | 88px | -
--td-navbar-center-left | @navbar-right | -
--td-navbar-center-width | 187px | -
--td-navbar-color | @text-color-primary | -
--td-navbar-height | 48px | -
--td-navbar-left-arrow-size | 24px | -
--td-navbar-left-max-width | --td-navbar-left-max-width | -
--td-navbar-title-font | @font-title-large | -
