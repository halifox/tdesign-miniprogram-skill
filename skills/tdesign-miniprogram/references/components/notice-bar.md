# NoticeBar 公告栏

在导航栏下方，用于给用户显示提示消息。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/notice-bar)。

> 该组件于 0.9.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/MEyzaMmo8I52)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 01 组件类型

纯文字的公告栏

```wxml
<t-notice-bar visible="{{true}}" prefixIcon="{{false}}">
  <view slot="content">这是一条普通的通知信息</view>
</t-notice-bar>

```
```js
Component({});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar"
  }
}

```

带图标的公告栏

~~~wxml
<t-notice-bar visible="{{visible}}" prefixIcon="{{false}}" content="提示文字描述提示文字描述提示文字描述">
  <view slot="prefix-icon">
    <t-icon name="error-circle-filled"></t-icon>
  </view>
</t-notice-bar>
~~~

~~~js
Component({
  data: {
    visible: true,
  },
});
~~~

~~~json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar",
    "t-icon": "tdesign-miniprogram/icon/icon"
  }
}
~~~

带关闭的公告栏

~~~wxml
<t-notice-bar
  visible="{{visible}}"
  suffixIcon="close"
  content="这是一条普通的通知信息"
  bind:click="click"
></t-notice-bar>
~~~

~~~js
Component({
  data: {
    visible: true,
  },

  methods: {
    click(e) {
      const { trigger } = e.detail;
      console.log(`click on the ${trigger} area`);
    },
  },
});
~~~

~~~json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar"
  }
}
~~~

带入口的公告栏

```wxml
<t-notice-bar visible="{{visible}}" suffixIcon="chevron-right" bind:click="click">
  <view slot="content" class="inline"> 这是一条普通的通知信息 </view>
  <t-link slot="operation" content="详情" theme="primary" underline="{{false}}" navigator-props="{{navigatorProps}}" />
</t-notice-bar>

<t-notice-bar
  visible="{{visible}}"
  suffixIcon="chevron-right"
  content="这是一条普通的通知信息"
  bind:click="click"
></t-notice-bar>

```
```js
Component({
  data: {
    visible: true,
    navigatorProps: {
      url: '/pages/xxx/xxx',
    },
  },

  methods: {
    click(e) {
      const { trigger } = e.detail;
      console.log(`click on the ${trigger} area`);
    },
  },
});

```
```wxss
.inline {
  display: inline;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar",
    "t-link": "tdesign-miniprogram/link/link"
  }
}

```

自定义样式的公告栏

```wxml
<t-notice-bar
  visible="{{true}}"
  prefixIcon="sound"
  suffixIcon="chevron-right"
  content="提示文字描述提示文字描述提示文字描述"
  t-class="external-class"
  t-class-prefix-icon="external-class-prefix-icon"
></t-notice-bar>

```
```js
Component({});

```
```wxss
page .external-class {
  opacity: 1;
  background: var(--td-bg-color-secondarycontainer, #f3f3f3);
}

page .external-class-prefix-icon {
  color: var(--td-text-color-primary);
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar"
  }
}

```

自定义内容的公告栏

```wxml
<!-- slot实现自定义content内容 -->
<t-notice-bar visible="{{true}}">
  <view slot="content" class="inline"> 提示文字描述提示文字描述提示文字描述提示文字描述提示文字描述提示文字描述 </view>
  <t-link slot="operation" content="详情" theme="primary" underline="{{false}}" navigator-props="{{navigatorProps}}" />
  <t-icon slot="suffix-icon" name="close" size="44rpx"></t-icon>
</t-notice-bar>

```
```js
Component({
  data: {
    navigatorProps: {
      url: '/pages/xxx/xxx',
    },
  },
});

```
```wxss
.inline {
  display: inline;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar",
    "t-link": "tdesign-miniprogram/link/link",
    "t-icon": "tdesign-miniprogram/icon/icon"
  }
}

```

### 02 组件状态

公告栏类型有普通（info）、警示（warning）、成功（success）、错误（error）

```wxml
<t-notice-bar visible="{{true}}" content="默认状态公告栏默认状态公告栏"></t-notice-bar>
<t-notice-bar visible="{{true}}" theme="success" content="成功状态公告栏成功状态公告栏"></t-notice-bar>
<t-notice-bar visible="{{true}}" theme="warning" content="警示状态公告栏警示状态公告栏"></t-notice-bar>
<t-notice-bar visible="{{true}}" theme="error" content="错误状态公告栏错误状态公告栏"></t-notice-bar>

```
```js
Component({});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar"
  }
}

```

### 03 可滚动公告栏

可滚动公告栏有水平（horizontal）和垂直（vertical）

```wxml
<t-notice-bar
  visible="{{visible}}"
  prefixIcon="{{false}}"
  marquee="{{marquee1}}"
  content="提示文字描述提示文字描述提示文字描述提示文字描述文"
></t-notice-bar>

<t-notice-bar
  visible="{{visible}}"
  marquee="{{marquee2}}"
  content="提示文字描述提示文字描述提示文字描述提示文字描述文"
></t-notice-bar>

<t-notice-bar
  visible="{{true}}"
  direction="vertical"
  interval="{{3000}}"
  content="{{content}}"
  prefixIcon="sound"
  bind:click="click"
></t-notice-bar>

```
```js
Component({
  data: {
    visible: true,
    marquee1: {
      speed: 80,
      loop: -1,
      delay: 0,
    },
    marquee2: {
      speed: 60,
      loop: -1,
      delay: 0,
    },
    content: ['君不见', '高堂明镜悲白发', '朝如青丝暮成雪', '人生得意须尽欢', '莫使金樽空对月'],
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-notice-bar": "tdesign-miniprogram/notice-bar/notice-bar"
  }
}

```


## API

### NoticeBar Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
content | String / Array | - | 文本内容 | N
direction | String | horizontal | 滚动方向。可选项：horizontal/vertical | N
interval | Number | 2000 | 间隔时间【仅在 direction='vertical' 有效】 | N
marquee | Boolean / Object | false | 跑马灯效果。speed 指速度控制；loop 指循环播放次数，值为 -1 表示循环播放，值为 0 表示不循环播放；delay 表示延迟多久开始播放【仅在 direction='horizontal' 有效】。TS 类型：`boolean \| NoticeBarMarquee` `interface NoticeBarMarquee { speed?: number; loop?: number; delay?: number }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/notice-bar/type.ts) | N
operation | String | - | 右侧额外信息 | N
prefix-icon | String / Boolean / Object | true | 前缀图标。值为字符串表示图标名称，值为 `false` 表示不显示前缀图标，值为 `Object` 类型，表示透传至 `icon`，不传表示使用主题图标 | N
suffix-icon | String / Object | - | 后缀图标。值为字符串表示图标名称。值为 `Object` 类型，表示透传至 `icon`，不传表示不显示后缀图标 | N
theme | String | info | 内置主题。可选项：info/success/warning/error | N
visible | Boolean | false | 显示/隐藏 | N
default-visible | Boolean | undefined | 显示/隐藏。非受控属性 | N

### NoticeBar Events

名称 | 参数 | 描述
-- | -- | --
change | `(current: number, source: '' \| 'autoplay' \| 'touch')` | 当 `direction="vertical"` 时轮播切换时触发
click | `(trigger: NoticeBarTrigger)` | 点击事件。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/notice-bar/type.ts)。<br/>`type NoticeBarTrigger = 'prefix-icon' \| 'content' \| 'operation' \| 'suffix-icon';`<br/>

### NoticeBar Slots

名称 | 描述
-- | --
content | 文本内容
operation | 自定义 `operation` 显示内容
prefix-icon | 前缀图标
suffix-icon | 后缀图标

### NoticeBar External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-content | 内容样式类
t-class-operation | 右侧额外信息样式类
t-class-prefix-icon | 前置图标样式类
t-class-suffix-icon | 后置图标样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-notice-bar-error-bg-color | @error-color-1 | -
--td-notice-bar-error-color | @error-color | -
--td-notice-bar-font-color | @text-color-primary | -
--td-notice-bar-info-bg-color | @brand-color-light | -
--td-notice-bar-info-color | @brand-color | -
--td-notice-bar-operation-font-color | @brand-color | -
--td-notice-bar-success-bg-color | @success-color-1 | -
--td-notice-bar-success-color | @success-color | -
--td-notice-bar-suffix-icon-color | @text-color-placeholder | -
--td-notice-bar-warning-bg-color | @warning-color-1 | -
--td-notice-bar-warning-color | @warning-color | -
