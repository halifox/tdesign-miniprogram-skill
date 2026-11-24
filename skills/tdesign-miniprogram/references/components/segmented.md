# Segmented 分段控制器

用于展示多个选项并允许用户选择其中单个选项。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/segmented)。

> 该组件于 1.14.0 版本上线，请留意版本
> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-segmented": "tdesign-miniprogram/segmented/segmented"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/Io87zBm98p8P)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 组件类型

基础

```wxml
<view class="example-segmented">
  <t-segmented options="{{options}}" default-value="{{0}}" />
</view>

<view class="example-segmented">
  <t-segmented options="{{optionsWithIcon}}" value="{{valueWithIcon}}" bind:change="onChangeWithIcon" />
</view>

```
```js
Component({
  data: {
    options: [
      { value: 0, label: '选项' },
      { value: 1, label: '选项' },
      { value: 2, label: '选项' },
    ],
    valueWithIcon: 0,
    optionsWithIcon: [
      { value: 0, label: '选项', icon: 'home' },
      { value: 1, label: '选项', icon: 'home' },
      { value: 2, label: '选项', icon: 'home' },
    ],
  },
  methods: {
    onChangeWithIcon(e) {
      console.log('onChangeWithIcon:', e.detail);
      this.setData({ valueWithIcon: e.detail.value });
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-segmented": "tdesign-miniprogram/segmented/segmented"
  }
}

```

自适应宽度

```wxml
<view class="example-segmented">
  <t-segmented block options="{{options}}" default-value="{{0}}" />
</view>

<view class="example-segmented">
  <t-segmented block options="{{optionsWithIcon}}" value="{{valueWithIcon}}" bind:change="onChangeWithIcon" />
</view>

```
```js
Component({
  data: {
    options: [
      { value: 0, label: '选项' },
      { value: 1, label: '选项' },
      { value: 2, label: '选项' },
    ],
    valueWithIcon: 0,
    optionsWithIcon: [
      { value: 0, label: '选项', icon: 'home' },
      { value: 1, label: '选项', icon: 'home' },
      { value: 2, label: '选项', icon: 'home' },
    ],
  },
  methods: {
    onChangeWithIcon(e) {
      console.log('onChangeWithIcon:', e.detail);
      this.setData({ valueWithIcon: e.detail.value });
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-segmented": "tdesign-miniprogram/segmented/segmented"
  }
}

```

### 组件状态

控制器禁用态

```wxml
<view class="example-segmented">
  <t-segmented options="{{optionsWithDisabled}}" value="{{valueWithDisabled}}" bind:change="onChangeWithDisabled" />
</view>

```
```js
Component({
  data: {
    valueWithDisabled: 0,
    optionsWithDisabled: [
      { value: 0, label: '选中' },
      { value: 1, label: '默认' },
      { value: 2, label: '禁用', disabled: true },
    ],
  },
  methods: {
    onChangeWithDisabled(e) {
      console.log('onChangeWithDisabled:', e.detail);
      this.setData({ valueWithDisabled: e.detail.value });
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-segmented": "tdesign-miniprogram/segmented/segmented"
  }
}

```


## API

### Segmented Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
block | Boolean | false | 是否撑满父元素宽度 | N
disabled | Boolean | - | 是否禁用 | N
options | Object | [] | 数据化配置选项内容。TS 类型：`string[] \| number[] \| SegmentedItem[] ` `interface SegmentedItem { value: string \| number; label?: string; icon?: string \| object; disabled?: boolean }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/segmented/type.ts) | N
value | String / Number | - | 当前选中的值 | N
default-value | String / Number | undefined | 当前选中的值。非受控属性 | N

### Segmented Events

名称 | 参数 | 描述
-- | -- | --
change | `(detail: { value: string \| number, selectedOption: SegmentedItem })` | 选项值发生变化时触发

### Segmented External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-item | 列表子项样式类
t-class-thumb | 动画背景样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-segmented-bg-color | @bg-color-component-disabled | -
--td-segmented-item-active-bg | @bg-color-container | -
--td-segmented-item-active-color | @brand-color | -
--td-segmented-item-color | @text-color-primary | -
--td-segmented-item-disabled-color | @text-color-disabled | -
--td-segmented-item-label-font | @font-body-medium | -
--td-segmented-transition | all @anim-duration-base @anim-time-fn-easing | -
