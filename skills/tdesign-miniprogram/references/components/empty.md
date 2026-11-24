# Empty 空状态

用于空状态时的占位提示。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/empty)。

> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-empty": "tdesign-miniprogram/empty/empty"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/7OvyJMmt8i5y)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 类型

图标空状态

```wxml
<t-empty icon="info-circle-filled" description="描述文字" />

```
```js
Component({});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-empty": "tdesign-miniprogram/empty/empty"
  }
}

```

自定义图片空状态

~~~wxml
<t-empty t-class="empty-cls" t-class-image="t-empty__image" image="{{image}}" description="描述文字" />
~~~

~~~js
Component({
  data: {
    image: 'https://tdesign.gtimg.com/mobile/demos/empty1.png',
  },
});
~~~

~~~wxss
.t-empty__image {
  width: 240rpx !important;
  height: 240rpx !important;
}
~~~

~~~json
{
  "component": true,
  "usingComponents": {
    "t-empty": "tdesign-miniprogram/empty/empty"
  }
}
~~~

带操作空状态

~~~wxml
<t-empty icon="info-circle-filled" description="描述文字">
  <t-button slot="action" theme="primary" size="large">操作按钮</t-button>
</t-empty>
~~~

~~~js
Component({});
~~~

~~~json
{
  "component": true,
  "usingComponents": {
    "t-empty": "tdesign-miniprogram/empty/empty",
    "t-button": "tdesign-miniprogram/button/button"
  }
}
~~~



## API

### Empty Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
description | String | - | 描述文字 | N
icon | String / Object | - | 图标名称。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon` | N
image | String | - | 图片地址 | N

### Empty Slots

名称 | 描述
-- | --
action | 操作按钮
description | 自定义 `description` 显示内容
image | 自定义 `image` 显示内容

### Empty External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-description | 描述样式类
t-class-image | 图片样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-empty-action-margin-top | @spacer-4 | -
--td-empty-description-color | @text-color-placeholder | -
--td-empty-description-font | @font-body-medium | -
--td-empty-description-margin-top | @spacer-2 | -
--td-empty-icon-color | @text-color-placeholder | -
