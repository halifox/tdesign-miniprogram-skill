# Typography 排版

排版用于文本基础编排和样式，使用排版组件，可以快速完成页面中的文本内容制作，同时配合其他组件完成深色与浅色模式切换等风格统一的需求。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/typography)。

> 该组件于 1.15.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-paragraph": "tdesign-miniprogram/paragraph/paragraph",
  "t-text": "tdesign-miniprogram/text/text",
  "t-title": "tdesign-miniprogram/title/title"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/sX5kIfmO8t96)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 基础文本

```wxml
<view class="typography-example">
  <t-typography-text content="TDesign 是腾讯各业务团队在服务业务过程中沉淀的一套企业级设计体系。" />
</view>

```
```js
Component({});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-typography-text": "tdesign-miniprogram/text/text"
  }
}

```

### 组合用法

```wxml
<view class="typography-example typography-example--inline">
  <t-typography-title content="What is TDesign" />
  <t-typography-text
    mark
    content="TDesign is an enterprise-level design system accumulated by Tencent's various business teams."
  />
  <t-typography-paragraph>
    <t-typography-text strong>
      TDesign features a unified design values, consistent design language, and visual style, helping users form
      continuous and coherent perceptions of the experience.
    </t-typography-text>
    Based on this, TDesign offers out-typography-of-the-box UI component libraries, design guidelines, and design
    assets, elegantly and efficiently freeing design and development from repetitive tasks. Simultaneously, it
    facilitates easy extension on top of TDesign, enabling a better alignment with business requirements.
  </t-typography-paragraph>

  <t-typography-title>Comprehensive</t-typography-title>
  <t-typography-paragraph>
    TDesign Support
    <t-typography-text code>Vue 2</t-typography-text>, <t-typography-text code>Vue 3</t-typography-text>,
    <t-typography-text code>React</t-typography-text>
    components for Desktop Application and
    <t-typography-text code>Vue 3</t-typography-text>,
    <t-typography-text code>Wechat MiniProgram</t-typography-text>
    components for Mobile Application.
  </t-typography-paragraph>
  <t-typography-paragraph>
    <view>• Features</view>
    <view>• Comprehensive</view>
    <view style="padding-left: 24rpx">• Consistency</view>
    <view style="padding-left: 24rpx">• Usability</view>
    <view>• Join TDesign</view>
  </t-typography-paragraph>
  <t-typography-paragraph>
    <view>1. Features</view>
    <view>2. Comprehensive</view>
    <view style="padding-left: 24rpx">1. Consistency</view>
    <view style="padding-left: 24rpx">2. Usability</view>
    <view>3. Join TDesign</view>
  </t-typography-paragraph>
</view>

```
```js
Component({});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-typography-text": "tdesign-miniprogram/text/text",
    "t-typography-title": "tdesign-miniprogram/title/title",
    "t-typography-paragraph": "tdesign-miniprogram/paragraph/paragraph"
  }
}

```

### 主题样式

```wxml
<view class="typography-example typography-example--theme">
  <t-typography-text theme="primary" content="主色" />
  <t-typography-text theme="success" content="成功" />
  <t-typography-text theme="warning" content="警告" />
  <t-typography-text theme="error" content="错误" />
  <t-typography-text mark content="标记" />
</view>

```
```js
Component({});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-typography-text": "tdesign-miniprogram/text/text"
  }
}

```

### 可复制

```wxml
<view class="typography-example typography-example--border">
  <t-typography-text copyable content="这是一段可复制的文本" />
</view>

<view class="typography-example">
  <t-typography-text copyable="{{copyableCustomSuffix}}" content="这是一段带自定义图标的可复制的文本">
    <t-icon slot="suffix" name="smile" color="#0052D9" />
  </t-typography-text>
</view>

```
```js
Component({
  data: {
    copyableCustomSuffix: {
      suffix: true,
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-typography-text": "tdesign-miniprogram/text/text",
    "t-icon": "tdesign-miniprogram/icon/icon"
  }
}

```

### 文本省略

```wxml
<view class="typography-example typography-example--border">
  <t-typography-paragraph ellipsis content="{{content}}" />
</view>

<view class="typography-example typography-example--border">
  <t-typography-paragraph ellipsis="{{ellipsisExpandable}}" content="{{content}}" />
</view>

<view class="typography-example">
  <t-typography-paragraph ellipsis="{{ellipsisCustomSuffix}}" content="{{content}}">
    <t-icon slot="suffix" name="chevron-down" />
  </t-typography-paragraph>
</view>

```
```js
Component({
  data: {
    content:
      'TDesign 秉承开放的设计理念从创立之初就采用开源协作的方式进行设计和开发。协作方案讨论、组件设计以及 API 设计，包括源代码在内均在公司内部完全开放，赢得了内部开发者和设计师的广泛关注。TDesign 遵循平等、开放、严格的原则，不论参与者的角色如何。',
    ellipsisExpandable: {
      row: 2,
      expandable: true,
      collapsible: true,
    },
    ellipsisCustomSuffix: {
      row: 1,
      expandable: true,
      collapsible: false,
      suffix: true,
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-typography-paragraph": "tdesign-miniprogram/paragraph/paragraph",
    "t-icon": "tdesign-miniprogram/icon/icon"
  }
}

```


## API


### Paragraph Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
content | String | - | 段落内容 | N
ellipsis | Boolean / Object | false | 是否省略展示，可通过配置参数自定义省略操作的具体功能和样式。TS 类型：`boolean \| TypographyEllipsis `，[Text API Documents](https://tdesign.tencent.com/miniprogram/components/text?tab=api)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/paragraph/type.ts) | N

### Paragraph Slots

名称 | 描述
-- | --
content | 自定义 `content` 显示内容


### Text Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
code | Boolean | false | 是否添加代码样式 | N
content | String | - | 文本内容 | N
copyable | Boolean / Object | false | 是否可复制，值为 null 时表示使用 copyable 插槽自定义复制图标。TS 类型：`boolean \| TypographyCopyable \| null` `interface TypographyCopyable { text?: string }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/text/type.ts) | N
delete | Boolean | false | 是否添加删除线样式 | N
disabled | Boolean | false | 是否添加不可用样式 | N
ellipsis | Boolean / Object | false | 是否省略展示，可通过配置参数自定义省略操作的具体功能和样式。TS 类型：`boolean \| TypographyEllipsis ` `interface TypographyEllipsis { collapsible?: boolean; expandable?: boolean; row?: number;}`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/text/type.ts) | N
italic | Boolean | false | 文本是否为斜体 | N
keyboard | Boolean | false | 是否添加键盘样式 | N
mark | String / Boolean | false | 是否添加标记样式，默认为黄色，可通过配置颜色修改标记样式，如#0052D9 | N
strong | Boolean | false | 文本是否加粗 | N
theme | String | - | 主题。可选项：primary/secondary/success/warning/error | N
underline | Boolean | false | 是否添加下划线样式 | N

### Text Slots

名称 | 描述
-- | --
content | 自定义 `content` 显示内容


### Title Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
content | String | - | 段落内容 | N
ellipsis | Boolean / Object | false | 是否省略展示，可通过配置参数自定义省略操作的具体功能和样式。TS 类型：`boolean \| TypographyEllipsis `，[Text API Documents](https://tdesign.tencent.com/miniprogram/components/text?tab=api)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/title/type.ts) | N
level | String | h1 | 标题等级。可选项：h1/h2/h3/h4/h5/h6 | N

### Title Slots

名称 | 描述
-- | --
content | 自定义 `content` 显示内容
