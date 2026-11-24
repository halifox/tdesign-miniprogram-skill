# Popover 弹出气泡

用于文字提示的气泡框。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/popover)。

> 该组件于 1.12.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-popover": "tdesign-miniprogram/popover/popover"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/cHy4BMm78S5X)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 组件类型
#### 带箭头的弹出气泡

```wxml
<view class="row">
  <view class="demo-block__header-desc">带箭头的弹出气泡</view>
  <t-popover
    placement="top"
    theme="dark"
    bind:visible-change="onVisibleChange"
    data-target="normal"
    visible="{{visible.normal}}"
    closeOnClickOutside="{{false}}"
  >
    <view slot="content">弹出气泡内容</view>
    <view class="popover-example__content">
      <t-button theme="primary" variant="outline" size="large" data-target="normal" bind:tap="showPopover">
        带箭头
      </t-button>
    </view>
  </t-popover>

  <view class="demo-block__header-desc" style="margin-top: 32rpx">不带箭头的弹出气泡</view>
  <t-popover
    placement="top"
    theme="dark"
    content="弹出气泡内容"
    showArrow="{{false}}"
    bind:visible-change="onVisibleChange"
    data-target="noArrow"
    visible="{{visible.noArrow}}"
  >
    <view class="popover-example__content">
      <t-button theme="primary" variant="outline" size="large" data-target="noArrow" bind:tap="showPopover">
        不带箭头
      </t-button>
    </view>
  </t-popover>

  <view class="demo-block__header-desc" style="margin-top: 32rpx">自定义内容弹出气泡</view>
  <view class="custom">
    <t-popover
      placement="top"
      theme="dark"
      visible="{{visible.custom}}"
      data-target="custom"
      bind:visible-change="onVisibleChange"
    >
      <view slot="content">
        <view class="custom__list">
          <view wx:for="{{3}}" wx:key="index" class="custom__item">选项{{ index + 1 }}</view>
        </view>
      </view>

      <view class="popover-example__content">
        <t-button theme="primary" variant="outline" size="large" data-target="custom" bind:tap="showPopover">
          自定义内容
        </t-button>
      </view>
    </t-popover></view
  >
</view>

```
```js
Component({
  data: {
    visible: {
      normal: false,
      noArrow: false,
      custom: false,
    },
  },
  methods: {
    showPopover(e) {
      const { target } = e.currentTarget.dataset;
      this.setData({
        [`visible.${target}`]: !this.data.visible[target],
      });
    },
    onVisibleChange(e) {
      const { target } = e.currentTarget.dataset;
      this.setData({
        [`visible.${target}`]: e.detail.visible,
      });
    },
  },
});

```
```wxss
.row {
  display: flex;
  flex-direction: column;
}

.demo-block__header-desc {
  margin-top: var(--td-spacer, 16rpx);
  margin-bottom: 32rpx;
  font-size: var(--td-font-size-base, 28rpx);
  white-space: pre-line;
  color: var(--bg-color-demo-desc);
  line-height: 22px;
}

.popover-example__content {
  display: flex;
  justify-content: center;
}

.custom {
  display: flex;
  justify-content: center;
  --td-popover-padding: 0;
}

.custom__list {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #fff;
}

.custom__item {
  width: 105px;
  line-height: 24px;
  text-align: center;
  padding: 12px;
}

.custom__item:not(:last-child) {
  border-bottom: 1px solid #fff;
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-popover": "tdesign-miniprogram/popover/popover",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```

### 组件样式

#### 气泡主题
```wxml
<view class="row">
  <view class="popover-example__content">
    <t-popover
      placement="top"
      theme="dark"
      content="弹出气泡内容"
      visible="{{visible.dark}}"
      data-target="dark"
      bind:visible-change="onVisibleChange"
    >
      <t-button
        class="button-width--small"
        theme="primary"
        variant="outline"
        size="large"
        data-target="dark"
        bind:tap="showPopover"
      >
        深色
      </t-button>
    </t-popover>
  </view>
  <view class="popover-example__content">
    <t-popover
      placement="top"
      theme="light"
      content="弹出气泡内容"
      visible="{{visible.light}}"
      data-target="light"
      bind:visible-change="onVisibleChange"
    >
      <t-button
        class="button-width--small"
        theme="primary"
        variant="outline"
        size="large"
        data-target="light"
        bind:tap="showPopover"
      >
        浅色
      </t-button>
    </t-popover>
  </view>
  <view class="popover-example__content">
    <t-popover
      placement="top"
      theme="brand"
      content="弹出气泡内容"
      visible="{{visible.brand}}"
      data-target="brand"
      bind:visible-change="onVisibleChange"
    >
      <t-button
        class="button-width--small"
        theme="primary"
        variant="outline"
        size="large"
        data-target="brand"
        bind:tap="showPopover"
      >
        品牌色
      </t-button>
    </t-popover>
  </view>
</view>
<view class="row" style="margin-top: 32rpx">
  <view class="popover-example__content">
    <t-popover
      placement="top"
      theme="success"
      content="弹出气泡内容"
      visible="{{visible.success}}"
      data-target="success"
      bind:visible-change="onVisibleChange"
    >
      <t-button
        class="button-width--small"
        theme="primary"
        variant="outline"
        size="large"
        data-target="success"
        bind:tap="showPopover"
      >
        成功色
      </t-button>
    </t-popover>
  </view>
  <view class="popover-example__content">
    <t-popover
      placement="top"
      theme="warning"
      content="弹出气泡内容"
      visible="{{visible.warning}}"
      data-target="warning"
      bind:visible-change="onVisibleChange"
    >
      <t-button
        class="button-width--small"
        theme="primary"
        variant="outline"
        size="large"
        data-target="warning"
        bind:tap="showPopover"
      >
        警告色
      </t-button>
    </t-popover>
  </view>
  <view class="popover-example__content">
    <t-popover
      placement="top"
      theme="error"
      content="弹出气泡内容"
      visible="{{visible.error}}"
      data-target="error"
      bind:visible-change="onVisibleChange"
    >
      <t-button
        class="button-width--small"
        theme="primary"
        variant="outline"
        size="large"
        data-target="error"
        bind:tap="showPopover"
      >
        错误色
      </t-button>
    </t-popover>
  </view>
</view>

```
```js
Component({
  data: {
    visible: {
      dark: false,
      light: false,
      success: false,
      brand: false,
      warning: false,
      error: false,
    },
  },
  methods: {
    showPopover(e) {
      const { target } = e.currentTarget.dataset;
      this.setData({
        [`visible.${target}`]: !this.data.visible[target],
      });
    },
    onVisibleChange(e) {
      const { target } = e.currentTarget.dataset;
      this.setData({
        [`visible.${target}`]: e.detail.visible,
      });
    },
  },
});

```
```wxss
.row {
  display: flex;
  padding: 0 32rpx;
  gap: 32rpx;
}

.demo-block__header-desc {
  margin-top: var(--td-spacer, 16rpx);
  margin-bottom: 32rpx;
  font-size: var(--td-font-size-base, 28rpx);
  white-space: pre-line;
  color: var(--bg-color-demo-desc);
  line-height: 22px;
}

.popover-example__content {
  flex: 1;
}

.button-width--small {
  width: 204rpx;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-popover": "tdesign-miniprogram/popover/popover",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```

#### 气泡位置
```wxml
<view class="popover-example-row">
  <view class="demo-block__header-desc">顶部弹出气泡</view>
  <view class="row">
    <view class="popover-example__content">
      <t-popover
        placement="top-left"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="topLeft"
        visible="{{visible.topLeft}}"
      >
        <view slot="content">弹出气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-width--small"
            theme="primary"
            variant="outline"
            size="large"
            data-target="topLeft"
            bind:tap="showPopover"
          >
            顶部左
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="top"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="top"
        visible="{{visible.top}}"
      >
        <view slot="content">弹出气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-width--small"
            theme="primary"
            variant="outline"
            size="large"
            data-target="top"
            bind:tap="showPopover"
          >
            顶部中
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="top-right"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="topRight"
        visible="{{visible.topRight}}"
      >
        <view slot="content">弹出气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-width--small"
            theme="primary"
            variant="outline"
            size="large"
            data-target="topRight"
            bind:tap="showPopover"
          >
            顶部右
          </t-button>
        </view>
      </t-popover>
    </view>
  </view>
</view>

<view class="popover-example-row">
  <view class="demo-block__header-desc">底部弹出气泡</view>
  <view class="row">
    <view class="popover-example__content">
      <t-popover
        placement="bottom-left"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="bottomLeft"
        visible="{{visible.bottomLeft}}"
      >
        <view slot="content">弹出气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-width--small"
            theme="primary"
            variant="outline"
            size="large"
            data-target="bottomLeft"
            bind:tap="showPopover"
          >
            底部左
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="bottom"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="bottom"
        visible="{{visible.bottom}}"
      >
        <view slot="content">弹出气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-width--small"
            theme="primary"
            variant="outline"
            size="large"
            data-target="bottom"
            bind:tap="showPopover"
          >
            底部中
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="bottom-right"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="bottomRight"
        visible="{{visible.bottomRight}}"
      >
        <view slot="content">弹出气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-width--small"
            theme="primary"
            variant="outline"
            size="large"
            data-target="bottomRight"
            bind:tap="showPopover"
          >
            底部右
          </t-button>
        </view>
      </t-popover>
    </view>
  </view>
</view>

<view class="popover-example-row">
  <view class="demo-block__header-desc">右侧弹出气泡</view>
  <view class="column">
    <view class="popover-example__content">
      <t-popover
        placement="right-top"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="rightTop"
        visible="{{visible.rightTop}}"
      >
        <view slot="content">气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-with--large"
            theme="primary"
            variant="outline"
            size="large"
            data-target="rightTop"
            bind:tap="showPopover"
          >
            右侧上
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="right"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="right"
        visible="{{visible.right}}"
      >
        <view slot="content">气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-with--large"
            theme="primary"
            variant="outline"
            size="large"
            data-target="right"
            bind:tap="showPopover"
          >
            右侧中
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="right-bottom"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="rightBottom"
        visible="{{visible.rightBottom}}"
      >
        <view slot="content">气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-with--large"
            theme="primary"
            variant="outline"
            size="large"
            data-target="rightBottom"
            bind:tap="showPopover"
          >
            右侧下
          </t-button>
        </view>
      </t-popover>
    </view>
  </view>
</view>

<view class="flex-end popover-example-row">
  <view class="demo-block__header-desc">左侧弹出气泡</view>
  <view class="column">
    <view class="popover-example__content">
      <t-popover
        placement="left-top"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="leftTop"
        visible="{{visible.leftTop}}"
      >
        <view slot="content">气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-with--large"
            theme="primary"
            variant="outline"
            size="large"
            data-target="leftTop"
            bind:tap="showPopover"
          >
            左侧上
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="left"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="left"
        visible="{{visible.left}}"
      >
        <view slot="content">气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-with--large"
            theme="primary"
            variant="outline"
            size="large"
            data-target="left"
            bind:tap="showPopover"
          >
            左侧中
          </t-button>
        </view>
      </t-popover>
    </view>
    <view class="popover-example__content">
      <t-popover
        placement="left-bottom"
        theme="dark"
        bind:visible-change="onVisibleChange"
        data-target="leftBottom"
        visible="{{visible.leftBottom}}"
      >
        <view slot="content">气泡内容</view>
        <view class="popover-example__content">
          <t-button
            class="button-with--large"
            theme="primary"
            variant="outline"
            size="large"
            data-target="leftBottom"
            bind:tap="showPopover"
          >
            左侧下
          </t-button>
        </view>
      </t-popover>
    </view>
  </view>
</view>

```
```js
Component({
  data: {
    visible: {
      topLeft: false,
      top: false,
      topRight: false,
      bottomLeft: false,
      bottom: false,
      bottomRight: false,
      leftTop: false,
      left: false,
      leftBottom: false,
      rightTop: false,
      right: false,
      rightBottom: false,
    },
  },
  methods: {
    showPopover(e) {
      const { target } = e.currentTarget.dataset;
      this.setData({
        [`visible.${target}`]: !this.data.visible[target],
      });
    },
    onVisibleChange(e) {
      const { target } = e.currentTarget.dataset;
      this.setData({
        [`visible.${target}`]: e.detail.visible,
      });
    },
  },
});

```
```wxss
.popover-example-row {
  display: flex;
  flex-direction: column;
  padding: 0 32rpx;
  margin-bottom: 48rpx;
}

.row {
  display: flex;
  flex-direction: row;
  gap: 32rpx;
}

.column {
  display: flex;
  flex-direction: column;
  gap: 32rpx;
}

.flex-end .column {
  align-items: flex-end;
}

.demo-block__header-desc {
  margin-top: var(--td-spacer, 16rpx);
  margin-bottom: 32rpx;
  font-size: var(--td-font-size-base, 28rpx);
  white-space: pre-line;
  color: var(--bg-color-demo-desc);
  line-height: 22px;
}

.popover-example__content {
  flex: 1;
}

.button-width--small {
  width: 204rpx;
}

.button-with--large {
  width: 446rpx;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-popover": "tdesign-miniprogram/popover/popover",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```


## API

### Popover Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
close-on-click-outside | Boolean | true | 是否在点击外部元素后关闭菜单  | N
content | String | - | 确认框内容 | N
fixed | Boolean | false | `1.12.1`。如果触发元素为 `fixed` 场景，需要显示指定 `fixed` 属性为 `true`，同时需在触发元素层添加 `t-popover-wrapper--fixed` 类，用于定位触发元素  | N
placement | String | top | 浮层出现位置。可选项：top/left/right/bottom/top-left/top-right/bottom-left/bottom-right/left-top/left-bottom/right-top/right-bottom | N
show-arrow | Boolean | true | 是否显示浮层箭头 | N
theme | String | dark | 弹出气泡主题。可选项：dark/light/brand/success/warning/error | N
visible | Boolean | - | 是否显示气泡确认框 | N

### Popover Events

名称 | 参数 | 描述
-- | -- | --
visible-change | `(visible: boolean)` | 确认框显示或隐藏时触发

### Popover Slots

名称 | 描述
-- | --
\- | 默认插槽，用于自定义触发元素
content | 自定义 `content` 显示内容

### Popover External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-content | 内容样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-popover-brand-bg-color | @primary-color-1 | -
--td-popover-brand-color | @primary-color-7 | -
--td-popover-dark-bg-color | @font-gray-1 | -
--td-popover-dark-color | @text-color-anti | -
--td-popover-error-bg-color | @error-color-1 | -
--td-popover-error-color | @error-color-6 | -
--td-popover-light-bg-color | @bg-color-container | -
--td-popover-light-color | @text-color-primary | -
--td-popover-padding | @spacer-1 | -
--td-popover-success-bg-color | @success-color-1 | -
--td-popover-success-color | @success-color-5 | -
--td-popover-warning-bg-color | @warning-color-1 | -
--td-popover-warning-color | @warning-color-5 | -
