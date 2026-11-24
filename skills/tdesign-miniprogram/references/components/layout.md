# Layout 布局

以规则的网格阵列来指导和规范页面中的版面布局以及信息分布，提高界面内布局的一致性，节约成本。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/layout)。

> 该组件于 1.1.0 版本上线，请留意版本
> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-row": "tdesign-miniprogram/row/row",
  "t-col": "tdesign-miniprogram/col/col"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/yzXQPNmh8P5k)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"


### 组件类型

基础

```wxml
<t-row>
  <t-col span="8" t-class="dark">col-8</t-col>
  <t-col span="8" t-class="light">col-8</t-col>
  <t-col span="8" t-class="dark">col-8</t-col>
</t-row>

<t-row>
  <t-col span="4" t-class="dark">col-4</t-col>
  <t-col span="16" offset="4" t-class="light">col-16 col-offset-4</t-col>
</t-row>

<t-row>
  <t-col offset="12" span="12" t-class="dark">col-12 col-offset-12</t-col>
</t-row>

```
```js
Component({});

```
```wxss
.dark {
  background-color: #0052d9;
}

.light {
  background-color: #366ef4;
}

.dark,
.light {
  background-clip: content-box;
  color: #fff;
  font-size: 28rpx;
  line-height: 96rpx;
  margin-bottom: 32rpx;
  text-align: center;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-col": "tdesign-miniprogram/col/col",
    "t-row": "tdesign-miniprogram/row/row"
  }
}

```


增加间距

```wxml
<t-row gutter="16">
  <t-col span="8">
    <view class="dark">col-8</view>
  </t-col>
  <t-col span="8">
    <view class="dark">col-8</view>
  </t-col>
  <t-col span="8">
    <view class="dark">col-8</view>
  </t-col>
</t-row>

```
```js
Component({});

```
```wxss
.dark {
  background-color: #0052d9;
}

.light {
  background-color: #366ef4;
}

.dark,
.light {
  color: #fff;
  font-size: 28rpx;
  line-height: 96rpx;
  margin-bottom: 32rpx;
  text-align: center;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-col": "tdesign-miniprogram/col/col",
    "t-row": "tdesign-miniprogram/row/row"
  }
}

```



## API

### Col Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
offset | String / Number | - | 列的偏移量（默认单位px） | N
span | String / Number | - | 列的宽度（默认单位px） | N


### Row Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
gutter | String / Number | - | 列之间的间距（默认单位px） | N
