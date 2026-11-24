# Result 结果

反馈结果状态。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/result)。

> 该组件于 0.16.0 版本上线，请留意版本
> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-result": "tdesign-miniprogram/result/result"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/gJzz5Mmu8m5g)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 组件类型

基础结果

```wxml
<view wx:for="{{resultList}}" wx:for-item="item" wx:key="index">
  <view class="demo-section__content">
    <t-result theme="{{item.theme}}" title="{{item.title}}" />
  </view>
</view>

```
```js
Component({
  data: {
    resultList: [
      {
        title: '成功状态',
        theme: 'success',
      },
      {
        title: '失败状态',
        theme: 'error',
      },
      {
        title: '警示状态',
        theme: 'warning',
      },
      {
        title: '默认状态',
        theme: 'default',
      },
    ],
  },
});

```
```wxss
.demo-section__content {
  margin-bottom: 96rpx;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-result": "tdesign-miniprogram/result/result"
  }
}

```

带描述的结果

```wxml
<view wx:for="{{resultList}}" wx:for-item="item" wx:key="index">
  <view class="demo-section__content">
    <t-result theme="{{item.theme}}" title="{{item.title}}" description="{{item.description}}" />
  </view>
</view>

```
```js
Component({
  data: {
    resultList: [
      {
        title: '成功状态',
        theme: 'success',
        description: '描述文字',
      },
      {
        title: '失败状态',
        theme: 'error',
        description: '描述文字',
      },
      {
        title: '警示状态',
        theme: 'warning',
        description: '描述文字',
      },
      {
        title: '默认状态',
        theme: 'default',
        description: '描述文字',
      },
    ],
  },
});

```
```wxss
.demo-section__content {
  margin-bottom: 96rpx;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-result": "tdesign-miniprogram/result/result"
  }
}

```

自定义结果

```wxml
<t-result t-class-image="external-class-image" image="https://tdesign.gtimg.com/mobile/demos/result1.png">
  <view slot="title"> 自定义结果 </view>
  <view slot="description"> 描述文字 </view>
</t-result>

```
```js
Component({});

```
```wxss
.external-class-image {
  width: 100px;
  height: 80px;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-result": "tdesign-miniprogram/result/result"
  }
}

```

## 常见问题

<details>
  <summary>
    本地图片无法正确引用?
    <span class="icon">👇</span>
  </summary>
  <p style="margin-top: 10px; color: rgba(0, 0, 0, .6)">
    建议使用绝对路径，而不是相对路径。绝对路径以 app.json 所在位置为基准。
  </p>
</details>

## API

### Result Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
description | String | - | 描述文字 | N
icon | String / Boolean / Object | true | 图标名称。值为字符串表示图标名称，值为 `false` 表示不显示图标，值为 `Object` 类型，表示透传至 `icon`，不传表示使用主题图标 | N
image | String | - | 图片地址 | N
theme | String | default | 内置主题。可选项：default/success/warning/error | N
title | String | '' | 标题 | N

### Result Slots

名称 | 描述
-- | --
description | 自定义 `description` 显示内容
image | 自定义 `image` 显示内容
title | 自定义 `title` 显示内容

### Result External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-description | 描述样式类
t-class-image | 图片样式类
t-class-title | 标题样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-result-description-color | @text-color-secondary | -
--td-result-description-font | @font-body-medium | -
--td-result-description-margin-top | @spacer | -
--td-result-icon-default-color | @brand-color | -
--td-result-icon-error-color | @error-color | -
--td-result-icon-success-color | @success-color | -
--td-result-icon-warning-color | @warning-color | -
--td-result-title-color | @text-color-primary | -
--td-result-title-font | @font-title-extraLarge | -
--td-result-title-margin-top | @spacer-1 | -
